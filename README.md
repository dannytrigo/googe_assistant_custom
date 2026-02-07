# Google Assistant (Labels Support) - HACS Custom Component

[![hacs_badge](https://img.shields.io/badge/HACS-Custom-orange.svg)](https://github.com/custom-components/hacs)

This is a fork of the official [Home Assistant Google Assistant integration](https://www.home-assistant.io/integrations/google_assistant) that adds support for exposing entities to Google Assistant using labels.

## What's Different

This custom component adds a single configuration option to the official Google Assistant integration:

- **`exposed_labels`**: Expose entities to Google Assistant by applying specific labels

All other features and configuration options remain the same as the [official integration](https://www.home-assistant.io/integrations/google_assistant).

## Installation via HACS

### Adding as a Custom Repository

1. Install HACS if you haven't already (follow the [official HACS installation guide](https://hacs.xyz/docs/setup/download))

2. Add this repository to HACS:
   - Open Home Assistant
   - Go to HACS in the sidebar
   - Click on the three dots menu in the top right corner
   - Select "Custom repositories"
   - Add the repository URL: `https://github.com/dannytrigo/googe_assistant_custom`
   - Select category: Integration
   - Click "Add"

3. Install the integration:
   - In HACS, search for "Google Assistant (Labels Support)"
   - Click on it and then click "Download"
   - Restart Home Assistant

## Configuration

This integration is configured via YAML in your `configuration.yaml` file. For full configuration documentation, see the [official Google Assistant documentation](https://www.home-assistant.io/integrations/google_assistant).

### Using the `exposed_labels` Option

The `exposed_labels` configuration option works similarly to `exposed_domains`, but uses labels instead of domains to determine which entities are exposed to Google Assistant.

```yaml
google_assistant:
  project_id: YOUR_PROJECT_ID
  service_account: !include SERVICE_ACCOUNT.json
  report_state: true
  
  # Expose entities with specific labels
  exposed_labels:
    - google_assistant
    - voice_control
```

Any entity with one of the specified labels will be exposed to Google Assistant.

### Applying Labels to Entities

1. Go to Settings → Labels
2. Create a label (e.g., "google_assistant")
3. Navigate to an entity you want to expose
4. Add the label to that entity
5. Sync devices with Google Assistant (say "Hey Google, sync my devices" or call the `google_assistant.request_sync` service)

### Complete Example

```yaml
google_assistant:
  project_id: your-project-id-123
  service_account: !include SERVICE_ACCOUNT.json
  report_state: true
  
  # Traditional domain-based exposure
  exposed_domains:
    - light
    - switch
  
  # New label-based exposure
  exposed_labels:
    - google_assistant
  
  # Entity-specific configuration still works as normal
  entity_config:
    light.kitchen:
      name: "Kitchen Lights"
      room: "Kitchen"
```

## Documentation

For all other configuration options, setup instructions, and troubleshooting, refer to the [official Google Assistant integration documentation](https://www.home-assistant.io/integrations/google_assistant).

## License

This project maintains the same license as the original Home Assistant project (Apache 2.0).

## Credits

- Original integration by the [Home Assistant team](https://github.com/home-assistant/core/tree/dev/homeassistant/components/google_assistant)
- Forked and modified to add `exposed_labels` support
