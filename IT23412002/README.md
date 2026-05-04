# Test Automation UI - Image Preview Test

A Playwright-based UI test automation script that verifies image preview functionality on web applications.

## Overview

This test automation suite validates whether image preview features work correctly when uploading PNG files to a web application. It uses Playwright to automate browser interactions and captures screenshots of test results.

## Features

- **Automated file upload**: Tests PNG file upload functionality
- **Preview detection**: Uses intelligent DOM scanning to detect if previews are rendered
- **Screenshot capture**: Captures full-page screenshots for both pass and fail scenarios
- **Results tracking**: Logs test results to a CSV file for reporting and analysis
- **Configurable parameters**: Supports custom URLs, timeouts, and output directories
- **Error handling**: Gracefully handles test failures with detailed error information

## Prerequisites

- Python 3.7+
- Playwright
- Required browsers (automatically installed with Playwright)

## Installation

1. Install dependencies:
```bash
pip install playwright
```

2. Install required browsers:
```bash
playwright install chromium
```

## Usage

### Basic Run

Run the test with default settings:
```bash
python image_preview_test.py
```

### Command-Line Options

```bash
python image_preview_test.py [OPTIONS]
```

| Option | Default | Description |
|--------|---------|-------------|
| `--url` | https://www.pixelssuite.com/convert-to-png | Target URL to test |
| `--png` | sample.png | Path to PNG file to upload |
| `--out-dir` | results | Directory for output screenshots |
| `--csv` | execution_results.csv | CSV file for test results |
| `--headless` | False | Run browser in headless mode |
| `--timeout-ms` | 60000 | Test timeout in milliseconds |
| `--slow-mo-ms` | 0 | Slow down browser actions (ms) |

### Examples

Run with custom URL and output directory:
```bash
python image_preview_test.py --url https://example.com/upload --out-dir my_results
```

Run in headless mode with a 30-second timeout:
```bash
python image_preview_test.py --headless --timeout-ms 30000
```

Use a specific PNG file:
```bash
python image_preview_test.py --png path/to/my_image.png
```

## Output

### Test Results

The script generates:

1. **CSV Report** (`execution_results.csv`):
   - file_type: Type of file tested (PNG)
   - file_path: Path to the uploaded file
   - preview_detected: Whether preview was detected (True/False)
   - status: Test result (PASS/FAIL)
   - screenshot: Path to the screenshot

2. **Screenshots**:
   - `preview_pass.png`: Screenshot when preview is detected
   - `preview_fail.png`: Screenshot when preview is not detected
   - `preview_error.png`: Screenshot when an error occurs

3. **Console Output**: Real-time test progress and results

## How It Works

1. **Initialization**: Configures Playwright browser and loads the target URL
2. **File Upload**: Locates the file input element and uploads the PNG file
3. **Preview Detection**: Uses DOM scanning to detect visible preview elements
4. **Result Capture**: Takes screenshots and records test outcome
5. **Reporting**: Appends results to the CSV file

## Project Structure

```
test_automation_ui/
├── image_preview_test.py          # Main test script
├── execution_results.csv          # Test results (auto-generated)
├── sample.png                     # Default test PNG file
├── results/                       # Output directory for screenshots
└── README.md                      # This file
```

## Preview Detection Logic

The test uses a sophisticated algorithm to detect previews:

1. Searches for elements containing "preview" text
2. Checks parent elements for visible media (img, canvas, svg, video)
3. Validates visibility using `getClientRects()` method
4. Searches up to 6 levels of parent elements

## Troubleshooting

### "File upload input was not found"
- Verify the target URL has a file input element
- Increase `--timeout-ms` if the page loads slowly
- Check if the website structure has changed

### Preview not detected
- The preview element may use different naming/structure
- Try adjusting the test with `--slow-mo-ms` to observe the page
- Inspect the HTML to verify preview elements exist

### Timeout errors
- Increase `--timeout-ms` for slow connections
- Run with `--headless false` to see browser activity
- Check network connectivity to the target URL

## Dependencies

- **playwright**: Browser automation library
- **pathlib**: Cross-platform file path handling
- **csv**: Results reporting
- **base64**: Default PNG encoding

## License

[Add your license here]

## Contributing

[Add contribution guidelines here]
