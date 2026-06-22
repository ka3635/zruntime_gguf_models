# Llama.cpp Flutter Models

Pre-exported Llama.cpp and export tools for the `flutter` package.

## Architecture

Model `.gguf` files and labels are stored as **GitHub Release assets** (not in git).
Only metadata (`index.json`, `versions.json`) and export scripts are in the repository.

```
Repository (git):
├── versions.json           # Available versions and latest
├── {version}/index.json    # Model metadata (URLs, hashes, sizes)
├── python/                 # Export tools
└── LICENSES/               # Model licenses

GitHub Releases:
├── v1.1.0/                 # Release assets for llama.cpp 1.0.1
│   ├── qwen3_vl_q4.gguf
│   ├── todbert.ort
│   ├── labels.txt
│   ├── bert_labels.txt
│   └── ...
├── v1.1.0/                 # Release assets for llama.cpp 1.1.0
└── v1.2.0/                 # Release assets for llama.cpp 1.2.0
```

## Quick Start

### Get Latest Version

```dart
// Fetch versions.json from the repo
final versionsUrl = 'https://raw.githubusercontent.com/ka3635/zruntime_gguf_models/main/versions.json';
final response = await http.get(Uri.parse(versionsUrl));
final versions = jsonDecode(response.body);
final latest = versions['latest'];  // e.g., "1.2.0"
```

### Fetch Model Index

```dart
// Use the version to get index.json (metadata with download URLs)
final indexUrl = 'https://raw.githubusercontent.com/ka3635/zruntime_gguf_models/main/$latest/index.json';
final indexResponse = await http.get(Uri.parse(indexUrl));
final index = jsonDecode(indexResponse.body);

// Each model entry has a remoteUrl pointing to the GitHub Release asset
final models = index['models'] as List;
final ggufModels = models.where((m) => m['backend'] == 'gguf').toList();
```

## Available Models

### Image Classification (mobilenet)

| Model | Backend | Description |
|-------|---------|-------------|
| `qwen3_vl_q4.gguf` | gguf | CPU-optimized, all platforms |

