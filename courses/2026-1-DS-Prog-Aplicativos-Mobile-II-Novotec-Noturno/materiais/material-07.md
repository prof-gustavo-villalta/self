---
layout: material
title: "Material 07 - GPS e Mapas"
---

# 🗺️ GPS e Mapas em Flutter

Guia completo para integrar geolocalização e mapas em aplicativos Flutter,
incluindo posição atual, tracking e exibição de mapas com Google Maps.

---

## Pacotes Necessários

```yaml
dependencies:
  flutter:
    sdk: flutter
  geolocator: ^10.1.0 # GPS e localização
  google_maps_flutter: ^2.5.0 # Mapas Google
  flutter_polyline_points: ^2.0.0 # Rotas (opcional)
```

---

## Configuração

### Android (AndroidManifest.xml)

```xml
<manifest>
    <!-- Permissões de localização -->
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION" />

    <!-- Para Android 10+ -->
    <uses-permission android:name="android.permission.FOREGROUND_SERVICE" />

    <application
        android:label="Meu App"
        android:name="${applicationName}"
        android:icon="@mipmap/ic_launcher">

        <!-- Chave da API Google Maps -->
        <meta-data
            android:name="com.google.android.geo.API_KEY"
            android:value="SUA_CHAVE_API_AQUI" />

        <activity ...>
            ...
        </activity>
    </application>
</manifest>
```

### Como obter a API Key

1. Acesse [Google Cloud Console](https://console.cloud.google.com/)
2. Crie um novo projeto ou selecione um existente
3. Ative a API "Maps SDK for Android"
4. Vá em "Credenciais" → "Criar Credenciais" → "Chave de API"
5. Restrinja a chave para Android (recomendado)

---

## Geolocator - Localização GPS

### Verificar Permissões

```dart
import 'package:geolocator/geolocator.dart';

class LocationService {
  // Verificar se o serviço está habilitado
  static Future<bool> isLocationEnabled() async {
    return await Geolocator.isLocationServiceEnabled();
  }

  // Verificar permissão
  static Future<LocationPermission> checkPermission() async {
    return await Geolocator.checkPermission();
  }

  // Solicitar permissão
  static Future<LocationPermission> requestPermission() async {
    return await Geolocator.requestPermission();
  }

  // Verificar e solicitar tudo
  static Future<bool> handlePermission() async {
    bool serviceEnabled = await isLocationEnabled();
    if (!serviceEnabled) {
      return false;
    }

    LocationPermission permission = await checkPermission();
    if (permission == LocationPermission.denied) {
      permission = await requestPermission();
      if (permission == LocationPermission.denied) {
        return false;
      }
    }

    if (permission == LocationPermission.deniedForever) {
      return false;
    }

    return true;
  }
}
```

### Obter Posição Atual

```dart
Future<void> _getCurrentLocation() async {
  final hasPermission = await LocationService.handlePermission();
  if (!hasPermission) return;

  try {
    Position position = await Geolocator.getCurrentPosition(
      desiredAccuracy: LocationAccuracy.high,
    );

    print('Latitude: ${position.latitude}');
    print('Longitude: ${position.longitude}');
    print('Altitude: ${position.altitude}');
    print('Precisão: ${position.accuracy}m');
    print('Velocidade: ${position.speed}m/s');

    setState(() {
      _currentPosition = position;
    });
  } catch (e) {
    print('Erro: $e');
  }
}
```

### Tracking em Tempo Real

```dart
StreamSubscription<Position>? _positionStream;

void _startTracking() {
  final LocationSettings locationSettings = LocationSettings(
    accuracy: LocationAccuracy.high,
    distanceFilter: 10,  // Atualizar a cada 10 metros
  );

  _positionStream = Geolocator.getPositionStream(
    locationSettings: locationSettings,
  ).listen((Position position) {
    print('Nova posição: ${position.latitude}, ${position.longitude}');

    setState(() {
      _currentPosition = position;
    });

    // Atualizar marcador no mapa
    _updateMarker(position);
  });
}

void _stopTracking() {
  _positionStream?.cancel();
}

@override
void dispose() {
  _stopTracking();
  super.dispose();
}
```

### Calcular Distância

```dart
double calculateDistance(
  double startLatitude,
  double startLongitude,
  double endLatitude,
  double endLongitude,
) {
  return Geolocator.distanceBetween(
    startLatitude,
    startLongitude,
    endLatitude,
    endLongitude,
  );
}

// Uso
final distancia = calculateDistance(
  -23.5505, -46.6333,  // São Paulo
  -22.9068, -43.1729,  // Rio de Janeiro
);
print('Distância: ${(distancia / 1000).toStringAsFixed(2)} km');
```

---

## Google Maps

### Mapa Básico

```dart
import 'package:google_maps_flutter/google_maps_flutter.dart';

class MapScreen extends StatefulWidget {
  const MapScreen({super.key});

  @override
  State<MapScreen> createState() => _MapScreenState();
}

class _MapScreenState extends State<MapScreen> {
  GoogleMapController? _mapController;

  // Posição inicial (São Paulo)
  static const LatLng _initialPosition = LatLng(-23.5505, -46.6333);

  Set<Marker> _markers = {};

  void _onMapCreated(GoogleMapController controller) {
    _mapController = controller;

    // Personalizar estilo do mapa (opcional)
    _mapController!.setMapStyle('''[
      {
        "featureType": "poi",
        "stylers": [{ "visibility": "off" }]
      }
    ]''');
  }

  void _addMarker(LatLng position) {
    setState(() {
      _markers.add(
        Marker(
          markerId: MarkerId(position.toString()),
          position: position,
          infoWindow: InfoWindow(
            title: 'Local',
            snippet: '${position.latitude}, ${position.longitude}',
          ),
          icon: BitmapDescriptor.defaultMarkerWithHue(
            BitmapDescriptor.hueRed,
          ),
        ),
      );
    });
  }

  Future<void> _goToCurrentLocation() async {
    final hasPermission = await LocationService.handlePermission();
    if (!hasPermission) return;

    final position = await Geolocator.getCurrentPosition();
    final target = LatLng(position.latitude, position.longitude);

    _mapController?.animateCamera(
      CameraUpdate.newCameraPosition(
        CameraPosition(
          target: target,
          zoom: 17,
          tilt: 30,
        ),
      ),
    );

    _addMarker(target);
  }

  @override
  void dispose() {
    _mapController?.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: GoogleMap(
        mapType: MapType.normal,
        initialCameraPosition: const CameraPosition(
          target: _initialPosition,
          zoom: 12,
        ),
        onMapCreated: _onMapCreated,
        markers: _markers,
        myLocationEnabled: true,
        myLocationButtonEnabled: false,
        zoomControlsEnabled: false,
        mapToolbarEnabled: false,
        onTap: _addMarker,
      ),
      floatingActionButton: Column(
        mainAxisAlignment: MainAxisAlignment.end,
        children: [
          FloatingActionButton.small(
            onPressed: () => _mapController?.animateCamera(
              CameraUpdate.zoomIn(),
            ),
            child: const Icon(Icons.add),
          ),
          const SizedBox(height: 8),
          FloatingActionButton.small(
            onPressed: () => _mapController?.animateCamera(
              CameraUpdate.zoomOut(),
            ),
            child: const Icon(Icons.remove),
          ),
          const SizedBox(height: 8),
          FloatingActionButton(
            onPressed: _goToCurrentLocation,
            child: const Icon(Icons.my_location),
          ),
        ],
      ),
    );
  }
}
```

### Mapa com Custom Markers

```dart
Future<BitmapDescriptor> _createCustomMarker(String text) async {
  // Criar marcador personalizado
  return BitmapDescriptor.defaultMarkerWithHue(
    BitmapDescriptor.hueBlue,
  );
}

// Marcador customizado com imagem
Future<BitmapDescriptor> _createMarkerFromAsset() async {
  return BitmapDescriptor.asset(
    const ImageConfiguration(size: Size(48, 48)),
    'assets/images/marker.png',
  );
}
```

### Círculos e Polígonos

```dart
Set<Circle> _circles = {
  Circle(
    circleId: CircleId('area'),
    center: LatLng(-23.5505, -46.6333),
    radius: 1000,  // metros
    fillColor: Colors.blue.withOpacity(0.3),
    strokeColor: Colors.blue,
    strokeWidth: 2,
  ),
};

Set<Polygon> _polygons = {
  Polygon(
    polygonId: PolygonId('regiao'),
    points: [
      LatLng(-23.55, -46.63),
      LatLng(-23.56, -46.63),
      LatLng(-23.56, -46.64),
      LatLng(-23.55, -46.64),
    ],
    fillColor: Colors.red.withOpacity(0.3),
    strokeColor: Colors.red,
    strokeWidth: 2,
  ),
};

// No GoogleMap:
GoogleMap(
  circles: _circles,
  polygons: _polygons,
  // ...
)
```

---

## Tela Completa de Exemplo

```dart
class LocationScreen extends StatefulWidget {
  const LocationScreen({super.key});

  @override
  State<LocationScreen> createState() => _LocationScreenState();
}

class _LocationScreenState extends State<LocationScreen> {
  Position? _currentPosition;
  String _address = '';
  bool _loading = false;

  Future<void> _getLocation() async {
    setState(() => _loading = true);

    try {
      final hasPermission = await LocationService.handlePermission();
      if (!hasPermission) {
        ScaffoldMessenger.of(context).showSnackBar(
          const SnackBar(content: Text('Permissão de localização negada')),
        );
        return;
      }

      final position = await Geolocator.getCurrentPosition(
        desiredAccuracy: LocationAccuracy.best,
      );

      setState(() {
        _currentPosition = position;
      });

      // Aqui você poderia usar geocoding para obter o endereço
      // usando o pacote geocoding

    } catch (e) {
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text('Erro: $e')),
      );
    } finally {
      setState(() => _loading = false);
    }
  }

  void _openMap() {
    if (_currentPosition == null) {
      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(content: Text('Obtenha a localização primeiro')),
      );
      return;
    }

    Navigator.push(
      context,
      MaterialPageRoute(
        builder: (_) => MapScreen(
          initialPosition: LatLng(
            _currentPosition!.latitude,
            _currentPosition!.longitude,
          ),
        ),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Minha Localização')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.stretch,
          children: [
            Card(
              child: Padding(
                padding: const EdgeInsets.all(16.0),
                child: Column(
                  children: [
                    const Icon(Icons.location_on, size: 64, color: Colors.red),
                    const SizedBox(height: 16),
                    if (_currentPosition != null) ...[
                      Text(
                        'Latitude: ${_currentPosition!.latitude.toStringAsFixed(6)}',
                        style: const TextStyle(fontSize: 18),
                      ),
                      Text(
                        'Longitude: ${_currentPosition!.longitude.toStringAsFixed(6)}',
                        style: const TextStyle(fontSize: 18),
                      ),
                      Text(
                        'Precisão: ${_currentPosition!.accuracy.toStringAsFixed(1)}m',
                        style: const TextStyle(fontSize: 16, color: Colors.grey),
                      ),
                    ] else ...[
                      const Text(
                        'Toque no botão abaixo para obter sua localização',
                        textAlign: TextAlign.center,
                      ),
                    ],
                  ],
                ),
              ),
            ),
            const SizedBox(height: 24),
            ElevatedButton.icon(
              onPressed: _loading ? null : _getLocation,
              icon: _loading
                ? const SizedBox(
                    width: 20,
                    height: 20,
                    child: CircularProgressIndicator(strokeWidth: 2),
                  )
                : const Icon(Icons.my_location),
              label: Text(_loading ? 'Obtendo...' : 'Obter Localização'),
            ),
            const SizedBox(height: 12),
            ElevatedButton.icon(
              onPressed: _currentPosition == null ? null : _openMap,
              icon: const Icon(Icons.map),
              label: const Text('Ver no Mapa'),
            ),
          ],
        ),
      ),
    );
  }
}
```

---

## Referências

- **geolocator**:
  [pub.dev/packages/geolocator](https://pub.dev/packages/geolocator)
- **google_maps_flutter**:
  [pub.dev/packages/google_maps_flutter](https://pub.dev/packages/google_maps_flutter)
- **Google Maps Platform**:
  [developers.google.com/maps](https://developers.google.com/maps/documentation/android-sdk/overview)
- \*\*Flutter Cookbook -
  Maps](https://docs.flutter.dev/cookbook/networking/fetch-data)

---

**Material elaborado para Mobile II - 2026**  
Prof. Gustavo Villalta
