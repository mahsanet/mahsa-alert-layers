# Mahsa Alert Data

Open snapshots of the [Mahsa Alert](https://mahsaalert.app) map layers in GeoJSON format, automatically published from the live database. Each layer is committed once per day, and only when its contents have actually changed.

## Structure

Each map layer is a single `FeatureCollection` file at the repository root, named by its layer key:

```text
newTargets.geojson
militaryBase.geojson
hospital.geojson
...
```

`state.json` is the manifest. It records the last publish time and a content hash per layer, so you can tell what changed without diffing the (large) GeoJSON files:

```json
{
  "lastUpdated": "2026-06-12T02:00:02.872Z",
  "layers": {
    "newTargets": "089af4c5539a5cfe0aac34c9d2bb133c656c18b5",
    "militaryBase": "4abf0118f21ed07f0940fd15c929b3deb71e14ec"
  }
}
```

Commit history is the change log: each daily export lands as a `data: YYYY-MM-DD (N layers changed)` commit touching only the layers that moved that day.

## Feature format

Every feature is a GeoJSON `Feature` with a `Point` (or polygon, for zones) geometry and a common property bag:

```json
{
  "type": "Feature",
  "geometry": { "type": "Point", "coordinates": [60.43494, 25.29910] },
  "properties": {
    "name:fa": "پایگاه دریایی کنارک",
    "city": "شهرستان کنارک",
    "province": "استان سیستان و بلوچستان",
    "date": "1772259045-1772382645",
    "status": "active",
    "publicId": "MzI6NzAyNzQ",
    "layerId": 32,
    "type": "location",
    "verificationTag": null,
    "createdAt": "2026-03-11T20:42:19.557Z",
    "updatedAt": "2026-03-31T03:39:09.263Z"
  }
}
```

Notable fields: `name:fa` (Farsi label), `date` (Unix epoch seconds, sometimes a `start-end` range), `publicId` (opens at `https://mahsaalert.app/fa/<publicId>`), and `verificationTag` (set when a feature originated from a citizen report).

## Layers

### Threat & security sites

| File | Description |
| --- | --- |
| `newTargets.geojson` | Confirmed strike targets |
| `targets.geojson` | Targets |
| `strikePoint.geojson` | Recorded strike points |
| `militaryBase.geojson` | Military zones |
| `basijBase.geojson` | Basij centers |
| `marakezEntezami.geojson` | Law-enforcement / police centers |
| `marakezGhazayi.geojson` | Judicial centers |
| `intelligence.geojson` | Intelligence facilities |
| `prisonPoly.geojson` | Prisons |
| `antiAirBase.geojson` | Air-defense sites |
| `radarBase.geojson` | Radar sites |
| `missilePrograms.geojson` | Missile-program sites |
| `nuclearPrograms.geojson` | Nuclear-program sites |
| `areowayBase.geojson` | Airbase / airfield sites |
| `unknownBase.geojson` | Unidentified bases |
| `cameraPoint.geojson` | Surveillance cameras |

### Civic & humanitarian

| File | Description |
| --- | --- |
| `citizenReport.geojson` | Citizen observational reports |
| `protestPoint.geojson` | Protest locations |
| `javidnam.geojson` | Javidnaman (those killed) memorials |
| `chelom.geojson` | Mourning-ceremony locations |
| `evacArea.geojson` / `evacAreaII.geojson` | Evacuation zones |
| `chatroom.geojson` | Community chat locations |

### Health & services

| File | Description |
| --- | --- |
| `hospital.geojson` | Hospitals |
| `clinic.geojson` | Clinics |
| `medicalClinic.geojson` | Medical clinics |
| `healthCenter.geojson` | Health centers |
| `pharmacy.geojson` | Pharmacies |
| `emergencyBase.geojson` | Emergency-service bases |
| `rescueBase.geojson` | Rescue bases |
| `redCrescent.geojson` | Red Crescent facilities |

### Other

| File | Description |
| --- | --- |
| `amakenMazhabiPoint.geojson` | Religious sites |
| `culturePoint.geojson` | Cultural sites |
| `zirsakht.geojson` | Infrastructure |

## Source

Data is exported daily from [mahsaalert.app](https://mahsaalert.app) — a platform tracking human rights incidents in Iran.

## License

This data is made available under the Creative Commons Attribution 4.0 International License (CC BY 4.0).
You are free to use, share, and adapt this data as long as you provide appropriate credit.

## Support this project

Access to the right information at the right moment can save lives.

Support the project:
https://gofund.me/1f800b407

Your donation helps extend the reach of life-saving alerts and critical safety information.
