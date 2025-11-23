# Home Assistant Add-on: Zigbee2MQTT Proxy

[![Docker Pulls](https://img.shields.io/docker/pulls/zigbee2mqtt/zigbee2mqtt-proxy-amd64.svg?style=flat-square&logo=docker)](https://cloud.docker.com/u/zigbee2mqtt/repository/docker/dwelch2101/zigbee2mqtt-proxy-amd64)

⚠️ This add-on does not contain Zigbee2MQTT ⚠️

This add-on acts as a proxy to an external running Zigbee2MQTT instance. 
The sole purpose of this add-on is to add a Zigbee2MQTT icon to the sidebar of Home Assistant which will open the frontend of an external running Zigbee2MQTT instance.

## Options

- `server` (required): this should be the URL on which the Zigbee2MQTT frontend is running, e.g. `http://192.168.2.43:8080` or `https://z2m.example.com`. Make sure there is no trailing slash! Both HTTP and HTTPS are supported.
- `auth_token` (optional): only use when you have an `auth_token` set for the frontend in the Zigbee2MQTT configuration.
- `ssl_verify` (optional, default: `true`): whether to verify SSL certificates when connecting to HTTPS servers. Set to `false` to accept self-signed certificates without providing a CA certificate.
- `ssl_certificate` (optional): filename of a custom CA certificate stored in the `/ssl` directory for verifying self-signed or locally-signed certificates. For example, if you have `/ssl/ca.crt`, set this to `ca.crt`.

## HTTPS Support

The proxy supports connecting to remote Zigbee2MQTT instances over HTTPS with the following configurations:

### Trusted Certificates (e.g., Let's Encrypt)
If your remote Zigbee2MQTT uses a certificate from a trusted CA:
```yaml
server: https://z2m.example.com
ssl_verify: true
```

### Self-Signed Certificates (without verification)
To accept self-signed certificates without validation:
```yaml
server: https://192.168.1.100:8443
ssl_verify: false
```

⚠️ **Warning**: Disabling SSL verification exposes you to man-in-the-middle attacks. Only use this in trusted networks.

### Self-Signed or Local CA Certificates (with verification)
For self-signed certificates or certificates signed by a local CA, place your CA certificate file in the Home Assistant `/ssl` directory and reference it:
```yaml
server: https://192.168.1.100:8443
ssl_verify: true
ssl_certificate: my-ca.crt
```

This provides secure connections with proper certificate validation.