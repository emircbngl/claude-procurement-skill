# Domain: Smart Home (IoT — hubs, sensors, switches, lighting, locks, cameras)

Ecosystem choice dominates everything. Pick the wrong protocol and you'll either replace gear or live with bridges forever.

## Research dimensions
- **functional_specs**: protocol (Matter / Zigbee / Z-Wave / Thread / Wi-Fi / Bluetooth LE / proprietary), power source (mains / battery / PoE), sensor type and range, response time, indoor / outdoor / weather rating (IP), local control fallback (works without cloud?), encryption / certification
- **quality_signals**: vendor security disclosure record, firmware update cadence, Mozilla Privacy Not Included rating, owner-reported bricking after cloud shutdowns, ecosystem app reliability
- **economic**: per-device cost + hub cost + subscription fee (some cameras/security charge $5–15/mo); battery replacement cadence; ongoing risk of brand EOL
- **usage_fit**: lighting / climate / security (cameras, alarms, locks) / energy monitoring / sensors / convenience automations / accessibility / pet monitoring

## Required user inputs (overrides universal)
- **Existing ecosystem** — Apple Home / Google Home / Alexa / Home Assistant / SmartThings (drives compatibility)
- **Renter vs owner** — affects ability to wire / install permanently
- **Wi-Fi infrastructure** — 2.4GHz coverage (most IoT lives here), capacity (hundreds of devices stress consumer routers)
- **Privacy posture** — cloud-dependent OK, or strict local-only required
- **Existing electrical** — neutral wire availability for smart switches (older homes lack), light fixture type (E27 / E14 / GU10 / can lights)

## Standards & compatibility axes

| Axis | Values | Compat rule |
|------|--------|-------------|
| **Protocol** | Matter (2.0+) — universal app-level standard; Zigbee 3.0 — mature mesh, needs hub; Z-Wave Plus / Long Range — mature mesh, needs hub, US/EU freq differs; Thread — IPv6 mesh, native Matter transport; Wi-Fi — no hub but congests network; BLE — short range, mostly accessories; proprietary RF (Lutron Caséta, Insteon legacy) | Matter is the future; Zigbee/Z-Wave are mature present; choose Matter-capable when possible |
| **Matter device class** | lights / plugs / switches / sensors / locks / thermostats / cameras (camera support added Matter 1.4) | Matter not yet universal across device classes; check class support per controller |
| **Frequency** | Zigbee: 2.4GHz (global); Z-Wave: 868MHz EU/TR, 908MHz US, 920MHz JP | Z-Wave devices region-locked — US Z-Wave won't work in TR |
| **Hub / border router** | Smart speakers (HomePod, Echo, Nest), Hubitat, SmartThings hub, Home Assistant + Zigbee/Z-Wave stick (zzh!, Sonoff Plus), Apple TV 4K (Thread border router) | Matter requires a border router; Apple/Google/Amazon each have their own; Home Assistant works with all |
| **Local control** | yes / cloud-only | Cloud-only = device bricks if vendor pulls support; Matter local + cloud is best |
| **Encryption** | TLS for cloud, AES for Zigbee/Z-Wave/Matter | Older devices may lack encryption; HSI cert good signal |
| **Wired switch neutral requirement** | yes / no | Many smart switches need neutral wire (newer wiring); some no-neutral options (Aqara, Lutron Caséta) for older homes |
| **Light bulb fitting** | E27, E14, GU10, B22, MR16 | Match existing fixture |
| **Camera storage** | Cloud (subscription), local SD, NAS via RTSP/ONVIF | RTSP/ONVIF lets cameras feed self-hosted (Frigate, Synology Surveillance Station) |
| **Smart lock** | Deadbolt / mortise / Euro cylinder / rim lock; key override; auto-lock | TR doors usually mortise + Euro cylinder; verify form factor — many smart locks are US deadbolt only |
| **Thermostat** | 24V (US HVAC), 230V (EU radiator/heat pump), TRV (radiator valve) | US Nest/Ecobee won't work on EU/TR heating typically; look for Tado, Drayton Wiser, Bosch, Honeywell EU lineup |

## Common pitfalls

- **Cloud-only IoT becomes paperweight** — Insteon went bankrupt 2022, devices bricked overnight. Wink, Iris by Lowes — same. Pick local-control or Matter.
- **Wi-Fi router melts under 100+ IoT devices** — consumer routers limited to ~50–100 clients; choose mesh systems built for IoT density or use Zigbee/Z-Wave for sensors.
- **Z-Wave region mismatch** — US-band Z-Wave devices unusable in TR/EU.
- **Smart lock incompatible with TR door** — most consumer smart locks are US Yale/Schlage deadbolt; for TR Euro cylinder, look at Yale Linus, Nuki, Tedee, Switchbot Lock.
- **Camera privacy / data sovereignty** — Ring (Amazon-owned) cooperates with US law enforcement; Eufy was caught uploading thumbnails to cloud despite "local-only" marketing. For privacy: choose local-only with NAS recording (Reolink, Amcrest, UniFi Protect, Hikvision with cloud disabled).
- **Battery sensor flood** — door/window sensors with CR2032 every 1–2yr × 30 sensors = expensive ongoing battery cost.
- **Aqara without Aqara hub** — many Aqara sensors require Aqara hub OR a Zigbee 3.0 hub (HA + Conbee/Sonoff). Direct Apple Home only via Aqara hub.
- **Wi-Fi smart bulbs flicker on slow networks** — Zigbee/Thread mesh much more reliable for lighting at scale.
- **HomeKit-only lock-in** — locks user into Apple; later move to Google = full replacement.

## Regional notes

- **Voice-assistant language support**: Apple Home / Google Home / Alexa each support a different set of languages; verify the user's primary language is supported by the chosen ecosystem.
- **Installer market depth**: pro-installed systems (KNX, Loxone, Crestron, Control4) require an integrator — verify availability in user's region. DIY-friendly platforms (Matter, Tuya, Home Assistant) work anywhere without local integrator.
- **Brand availability**: most major smart-home brands (Aqara, Sonoff, Philips Hue, Yeelight, Lutron Caseta) have global distribution; some (Lutron RA3, Insteon legacy, certain regional brands) are region-locked.
- **Wi-Fi router capacity**: regional ISP-supplied routers often weak; smart-home density may require user upgrade to mesh / business-grade router.

## B2B variant (commercial / hotel / office)
- Commercial-grade BMS (KNX, BACnet, Lutron) — different ecosystem from consumer; integrator required
- Centralized management (Cisco Meraki MR for Wi-Fi, KNX for lighting)
- PoE for power simplification (PoE+ for cameras, lighting, sensors)
- Multi-tenant access control, audit logging
- Compliance: regional data-privacy laws apply (GDPR / UK GDPR / CCPA-CPRA / LGPD / PDPA / PIPL / KVKK / APP, etc.) for camera footage and access logs — confirm vendor's DPA and any data-residency requirements per user's jurisdiction

## Trusted sources for web fallback

- [Matter spec](https://csa-iot.org/all-solutions/matter/) — official protocol
- [The Verge — smart home reviews](https://www.theverge.com/smart-home), [The Ambient](https://www.the-ambient.com)
- [Wirecutter smart home](https://www.nytimes.com/wirecutter/smart-home/)
- [Mozilla Privacy Not Included](https://foundation.mozilla.org/en/privacynotincluded/)
- [Home Assistant blog + community](https://community.home-assistant.io)
- [r/homeautomation](https://reddit.com/r/homeautomation), [r/homeassistant](https://reddit.com/r/homeassistant), [r/smarthome](https://reddit.com/r/smarthome)
- Brand sites with security/privacy disclosures (Aqara, Eufy post-2023 with improved disclosure)
