# Image-Based Text Adventure Generator

A Python application that transforms a collection of images into an interactive text adventure with branching storylines.

## Overview

This tool uses AI vision and language models to:
1. Analyze images from your collection
2. Generate engaging story segments based on each image
3. Create thematic connections between story segments
4. Build an interactive adventure with multiple paths and endings

The result is a set of markdown files that can be viewed as an interactive story where readers can make choices that lead to different narrative branches.

## Features

- **Image Analysis**: Uses the Gemma 2 vision model to extract detailed descriptions from images
- **Story Generation**: Creates narrative segments based on image content using Llama 3.3 language model
- **Thematic Coherence**: Identifies common themes across all story segments and rewrites content for consistency
- **Interactive Branching**: Automatically generates meaningful connections between story segments
- **Customizable Style**: Supports multiple narrative styles (adventure, mystery, fantasy, sci-fi)
- **Caching System**: Saves API responses to reduce processing time and costs on subsequent runs
- **Markdown Output**: Generates properly formatted markdown files with navigation links
- **Memory Management**: Processes images in batches with configurable delays to prevent memory issues

## Requirements

- Python 3.6+
- Ollama (version 0.1.16 or higher)
- Required Python packages (see requirements.txt):
  - ollama
  - pathlib
  - typing
  - requests
  - tqdm
  - pillow
  - pyyaml

## Installation

1. Clone this repository
2. Install required packages:
   ```
   pip install -r requirements.txt
   ```
3. Ensure Ollama is installed and running on your system
4. Download the required models:
   ```
   ollama pull gemma2:27b
   ollama pull llama3.3:latest
   ```

## Usage

### Basic Usage

```bash
python main.py
```

This will:
- Look for images in the default `input_images` directory
- Generate stories in the `_stories` directory
- Use the default "adventure" narrative style

### Command Line Options

```bash
python main.py --input INPUT_DIR --output OUTPUT_DIR --style STYLE --length WORD_COUNT --batch-size BATCH_SIZE --delay DELAY --start START_NUM --end END_NUM --config CONFIG_FILE --no-cache
```

- `--input`: Directory containing images (default: "input_images")
- `--output`: Directory for story files (default: "_stories")
- `--style`: Narrative style - "adventure", "mystery", "fantasy", or "sci-fi" (default: "adventure")
- `--length`: Approximate word count per story segment (default: 300)
- `--batch-size`: Number of images to process before taking a longer break (default: 10)
- `--delay`: Delay in seconds between processing images (default: 5)
- `--start`: Start processing from this image number (default: 1)
- `--end`: End processing at this image number (optional)
- `--config`: Path to JSON configuration file
- `--no-cache`: Disable caching of API responses

### Configuration File

You can customize the application by creating a JSON configuration file:

```json
{
  "input_dir": "my_images",
  "output_dir": "my_adventure",
  "vision_model": "gemma2:27b",
  "text_model": "llama3.3:latest",
  "story_length": 500,
  "temperature": 0.8,
  "narrative_style": "fantasy",
  "retry_attempts": 3,
  "retry_delay": 2,
  "batch_size": 5,
  "inter_image_delay": 10,
  "start_image": 1,
  "end_image": 20
}
```

## Output Structure

The generator creates:

1. An index.md file with:
   - A generated title for the overall adventure
   - A summary of themes
   - Links to all starting points

2. A markdown file for each image with:
   - A generated title
   - The image
   - A story segment
   - Links to connected story segments

## Troubleshooting

If you encounter issues while using the generator, please refer to the [Troubleshooting Guide](TROUBLESHOOTING.md) for solutions to common problems.

## Examples

### Example Script

An example script `example.sh` is provided to demonstrate different ways to use the generator:

```bash
# Make the script executable
chmod +x example.sh

# Run the example
./example.sh
```

The script shows how to:
- Process a subset of images to avoid memory issues
- Use different narrative styles
- Customize story length
- Use custom input and output directories
- Use a configuration file

### Sample Configuration

A sample configuration file `sample_config.json` is provided as a template:

```bash
# Run with the sample configuration
python main.py --config sample_config.json
```

### Output

After running the generator, open `_stories/index.md` to start the adventure. Each page will present a story segment with choices that lead to other segments, creating a branching narrative experience.

## Customization

- Add your own images to the input directory
- Modify the narrative style to change the tone and genre
- Adjust the story length to create shorter or longer segments
- Edit the prompts in the code to customize the story generation process


## Acknowledgments

This project uses:
- Ollama for local AI model hosting
- Gemma 2 for vision analysis
- Llama 3.3 for text generation
