# NZXT Kraken X2 and M2 coolers

## Capabilities by model and firmware version

| Model | Firmware versions | Coolant temperature | Static fan/pump control | Dynamic fan/pump control | Illumination control |
| :-- | :-: | :-: | :-: | :-: | :-: |
| M22 | all | no | no | no | yes |
| X[4-7]2 | < 3.0.0 | yes | yes | no | yes |
| X[4-7]2 | ≥ 3.0.0 | yes | instantaneous<sup>1</sup> | yes<sup>2</sup> | yes |

<sup>1</sup> After 5-10 seconds (FIXME) static fan/pump speeds are overridden
by the previously set fan/pump curves.  
<sup>2</sup> Dynamic fan/pump curves based on the coolant temperature.  

## USB & USB HID descriptors

TODO.

## Types of exchanges

TODO.

## Initialization

No-op.

## Retrieving status information

The cooler sends 16-byte status reports twice a second.

| Raw report slice | Description |
| :-: | :-- |
| 0x0 | Report ID: 0x04 |
| 0x1 | Coolant temperature, integer part, 1/9 °C |
| 0x2 | Coolant temperature, fractional part, 0.1 °C (FIXME) |
| 0x3–0x4 | Fan speed, big endian 2-byte integer, rpm |
| 0x5–0x6 | Pump speed, big endian 2-byte integer, rpm |
| 0xb | Firmware version, major number |
| 0xc–0xd | Firmware version, big endian 2-byte integer, minor number<sup>3</sup> |
| 0xe | Firmware version, patch number |

Only Kraken X models return valid coolant temperature, fan speed or pump speed
values.

<sup>3</sup> The minor number of the firmware version is *presumed* to be
specified as a 2-byte integer, but the second byte has not been necessary yet.

### Coolant temperature

The coolant temperature is encoded in two bytes, an integer part and a
fractional one.  The fractional part is probably base in decidegrees Celsius,
but some fractional values are never observed for certain integer parts.

| integer part | observed fractional parts |
| --- | --- |
| 32 | `123456789` |
| 33 | `1234 6789` |
| 34 | `123456789` |
| 35 | `1234 6789` |
| 36 | `12 45 789` |
| 37 | `1234 6789` |
| 38 | `12 45 789` |
| 39 | `12 45 789` |
