# WaifuTagger

A Python package for tagging anime-style images using SmilingWolf models. This package provides a simple interface to detect and tag various elements in anime/manga-style illustrations.

## Features

- Support for multiple SmilingWolf models
- Simple and batch image processing
- Flexible tag output formats
- Automatic threshold adjustment (MCut)
- Progress tracking for batch operations

## Installation

```bash
pip install waifutagger
```

## Quick Start

```python
from waifutagger import WaifuTagger

# Initialize tagger
tagger = WaifuTagger("eva02-large-v3")  # or any other available model

# Process single image
results = tagger.predict("image.jpg")

# Print tags
print(results['rating'])           # Image rating
print(results['general_tags'])     # General tags
print(results['character_tags'])   # Character tags

# Get formatted string
from waifutagger.formatters import format_tags
tags_string = format_tags(results)
print(tags_string)  # "rating_general, 1girl, solo, long_hair, ..."
```

## Available Models

- swinv2-v3: SmilingWolf/wd-swinv2-tagger-v3
- convnext-v3: SmilingWolf/wd-convnext-tagger-v3
- vit-v3: SmilingWolf/wd-vit-tagger-v3
- vit-large-v3: SmilingWolf/wd-vit-large-tagger-v3
- eva02-large-v3: SmilingWolf/wd-eva02-large-tagger-v3
- And more...

## Advanced Usage

### Batch Processing

```python
# Process multiple images
image_paths = ["img1.jpg", "img2.jpg", "img3.jpg"]
for img_path in image_paths:
    results = tagger.predict(img_path)
    # Save results
    with open(f"{img_path}_tags.txt", "w") as f:
        f.write(format_tags(results))
```

### Custom Thresholds

```python
# Use custom thresholds
results = tagger.predict(
    "image.jpg",
    general_threshold=0.4,    # Higher threshold for general tags
    character_threshold=0.9   # Higher threshold for character tags
)
```

### MCut Thresholding

```python
# Use automatic threshold adjustment
results = tagger.predict(
    "image.jpg",
    general_use_mcut=True,    # Use MCut for general tags
    character_use_mcut=True   # Use MCut for character tags
)
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

This package is based on the WaifuDiffusion tagger models by [SmilingWolf](https://huggingface.co/SmilingWolf).
