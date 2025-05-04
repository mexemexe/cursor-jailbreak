# Cursor Auto Accept: AI Code Suggestion Automation Tool

## Project Overview

Cursor Auto Accept is an intelligent automation tool designed to streamline the interaction with Cursor's AI code generation platform by automatically accepting AI suggestions. The project addresses the repetitive task of manually clicking "Accept" buttons when working with AI-generated code, providing developers with a seamless and efficient coding experience.

### Key Purpose

The tool automates the process of accepting AI code suggestions across multiple monitors, reducing manual intervention and allowing developers to maintain their workflow without interruption. It solves several common challenges in AI-assisted coding:

- Eliminating repetitive manual acceptance of code suggestions
- Supporting multi-monitor setups with per-monitor calibration
- Providing intelligent button detection with high accuracy

### Core Features

- **Multi-Monitor Support**: Calibrates and operates independently on different monitors
- **Intelligent Button Detection**: Uses advanced template matching with 80% confidence threshold
- **Adaptive Clicking**: Automatically identifies and clicks on AI suggestion accept buttons
- **Performance Management**: 
  - Rate-limited to 8 clicks per minute to prevent system overload
  - Restores cursor position after each click
  - Comprehensive logging for tracking bot activities

### Technical Highlights

- Utilizes computer vision techniques for button recognition
- Implements automatic calibration for precise button location
- Supports dynamic screen configuration
- Provides robust error handling and recovery mechanisms

The tool is particularly valuable for developers who frequently use AI code generation tools and want to minimize manual interaction, allowing them to focus more on coding and less on mechanical tasks.

## Getting Started, Installation, and Setup

### Prerequisites

Before getting started, ensure you have the following:
- Python 3.8 or higher
- Git
- A terminal or command line interface

### Quick Start

1. Clone the repository:
```bash
git clone https://github.com/yourusername/cursor-auto-accept.git
cd cursor-auto-accept
```

2. Run the setup script to prepare your environment:
```bash
./setup.sh
```

### Installation

#### System Requirements
- Supported Operating Systems: Linux, macOS
- Required Python Packages:
  - opencv-python (>=4.8.0)
  - numpy (>=1.24.0)
  - pyautogui (>=0.9.54)
  - pillow (>=10.0.0)
  - mss (>=9.0.1)

#### Virtual Environment Setup
The `setup.sh` script automatically:
- Creates necessary directories
- Sets up file permissions
- Creates a Python virtual environment
- Installs required dependencies

### Configuration and Calibration

Before using the bot, you must calibrate it for each monitor:

1. Stop any existing bot instances:
```bash
./stop_clickbot.sh
```

2. Activate the virtual environment:
```bash
source venv/bin/activate
```

3. Run calibration for all monitors:
```bash
python cursor_auto_accept.py --capture
```

Or for a specific monitor (0-based index):
```bash
python cursor_auto_accept.py --capture --monitor 0  # First monitor
python cursor_auto_accept.py --capture --monitor 1  # Second monitor
```

### Running the Bot

Start the bot:
```bash
./start_clickbot.sh
```

Stop the bot:
```bash
./stop_clickbot.sh
```

### Monitoring

Monitor bot activity via logs:
```bash
tail -f temp/logs/clickbot.log
```

### Development Mode

To run the bot in a development environment:
1. Activate the virtual environment
2. Run the main script directly:
```bash
source venv/bin/activate
python cursor_auto_accept.py
```

### Important Notes
- The bot has a built-in rate limit of 8 clicks per minute
- A minimum confidence threshold of 0.8 (80% match) is required for button detection
- Per-monitor calibration is essential for accurate performance

## Features / Capabilities

### Automated UI Interaction
- Intelligent screen scanning and template matching for automated UI interactions
- Multi-monitor support with dynamic monitor detection
- Configurable confidence threshold for match accuracy

### Advanced Image Recognition
- Precise template matching using computer vision techniques
- Supports multiple image template formats (PNG, JPG, JPEG)
- Adaptive screen region scanning

### Robust Error Handling
- Automated error state detection and recovery
- Graceful interrupt and signal handling
- Comprehensive logging and debug capabilities

### Customization Options
- Configurable scan interval
- Adjustable confidence threshold
- Debug mode for detailed logging and visual debugging

### Key Capabilities
- Automatic click generation based on image template matching
- Intelligent cooldown mechanism to prevent rapid clicking
- Periodic monitor rechecking to maintain application context

### Technical Features
- Cross-platform compatibility (uses mss for screen capture)
- Flexible configuration through command-line arguments
- Modular design with separate components for image matching, error recovery, and logging

## Usage Examples

### Basic Usage

Run the bot using the default configuration:

```bash
python3 main.py
```

### Command Line Options

The application supports several configuration options:

#### Debug Mode
Enable detailed logging and debug features:
```bash
python3 main.py --debug
```

#### Custom Scan Interval
Adjust the scan interval (default is 3.0 seconds):
```bash
python3 main.py --interval 5.0  # Scan every 5 seconds
```

#### Confidence Threshold
Modify the match confidence threshold (default is 0.8):
```bash
python3 main.py --confidence 0.7  # Lower confidence for more lenient matching
```

### Combining Options
You can combine multiple options:
```bash
python3 main.py --debug --interval 2.5 --confidence 0.75
```

### Startup Script
For convenience, use the provided startup script:
```bash
./run_bot.sh
```

#### Platform Support
- Supports running on macOS and Linux
- Automatically opens in a new terminal window on macOS
- Falls back to current terminal or xterm on other systems

### Important Notes
- Requires Python 3 and dependencies from `requirements.txt`
- Designed for automated UI interaction with image matching
- Configurable logging and error recovery mechanisms

## Project Structure

The project is organized into several key directories and files to support its functionality:

#### Main Components
- `main.py`: Central script for the primary application logic
- `clickbot.py`: Core implementation of the click automation bot
- `cursor_auto_accept.py`: Script for automatic acceptance functionality
- `error_recovery.py`: Module handling error recovery mechanisms
- `image_matcher.py`: Image matching and template recognition utilities

#### Configuration and Setup
- `requirements.txt`: List of Python package dependencies
- `setup.sh`: Setup script for project initialization
- `run_bot.sh`: Script to launch the bot
- `start_clickbot.sh`: Startup script for the click bot
- `stop_clickbot.sh`: Script to stop the click bot
- `logging_config.py`: Logging configuration management

#### Testing
- `test_clickbot.py`: Unit tests for the click bot
- `test_error_recovery.py`: Tests for error recovery functionality
- `test_matcher.py`: Tests for image matching capabilities
- `test_final.py`: Comprehensive final test suite

#### Assets and Resources
- `assets/`: Directory containing image assets and coordinate files
  - `monitor_0/`: Monitor-specific image and coordinate files
  - `backup/`: Backup copies of assets
- `debug/`: Debug-related images and diagnostic outputs
- `images/`: Additional project images and screenshots
- `temp/`: Temporary file storage
  - `logs/`: Log file storage

#### Additional Files
- `extension.js`: Potential browser or IDE extension script
- `cursor-plugin.json`: Configuration for cursor-related plugin
- `analyze_*.py`: Various analysis scripts (calibration, hover results)

#### Documentation
- `README.md`: Main project documentation
- `README_Prometheus.md`: Additional README for Prometheus-related information
- `cursor-instructions/`: Directory with development and process documentation
  - `features.md`
  - `github-process.md`
  - `notes.md`
  - `readme.md`
- `mvp-scope.md`: Minimum Viable Product scope document

## Technologies Used

### Programming Languages
- Python 3
- JavaScript (Node.js)

### Core Libraries and Frameworks
- OpenCV (opencv-python): Computer vision and image processing
- NumPy: Numerical computing and array operations
- PyAutoGUI: Desktop automation and GUI interaction
- Pillow (PIL): Image manipulation
- MSS: Cross-platform screen capture library

### Development and Testing Tools
- pytest (implied by test files): Unit testing framework
- Shell scripting (Bash)

### Extension Development
- Cursor IDE extension framework

### Operating System Compatibility
- Cross-platform (Linux/macOS/Windows implied by library choices)

## Additional Notes

### Performance Considerations

The Cursor Auto Accept bot is designed with careful attention to system performance and user experience:

- Rate-limited to prevent system overload (maximum 8 clicks per minute)
- Lightweight image processing using OpenCV and template matching
- Configurable confidence thresholds to minimize false positives
- Minimal system resource consumption

### Future Development Roadmap

The project has a clear vision for future enhancements, focusing on:

- Advanced multi-monitor support
- More robust button detection algorithms
- Enhanced UI for calibration and debugging
- Expanded configuration options
- Improved error handling and logging mechanisms

### Known Limitations

- Requires manual calibration for each monitor setup
- Depends on visual button recognition (may fail with UI changes)
- Performance can vary based on screen resolution and monitor configuration
- Requires Python 3.8+ environment

### Security and Privacy

- No external data transmission
- Operates entirely locally
- Uses system-level screenshot and mouse control libraries
- Minimal persistent data storage (only calibration images and logs)

### System Compatibility

Tested and verified on:
- Linux environments
- Multiple monitor configurations
- Varying screen resolutions

### Monitoring and Diagnostics

Comprehensive logging allows for detailed troubleshooting:
- Detailed click events recorded
- Error tracking
- Performance metrics
- Monitor-specific calibration logs

### Community and Contributions

This is an open-source project welcoming community contributions. Potential areas for improvement include:
- Cross-platform compatibility
- Additional monitor detection methods
- Enhanced machine learning-based button recognition

## Contributing

We welcome contributions to the project! To ensure a smooth collaboration, please follow these guidelines:

### Branch Strategy
- Create a new branch for each major feature or significant change
- Use a descriptive branch name that indicates the work being done
- Branches should be created from the main development branch

### Contribution Process
1. Fork the repository
2. Create a new branch for your feature or bugfix
3. Make your changes, following the project's existing code style
4. Write or update tests to cover your changes
5. Ensure all tests pass before submitting a pull request

### Testing
- All code contributions must include appropriate unit tests
- Run the existing test suite using `unittest` before submitting your pull request
- Ensure code coverage is maintained or improved

### Coding Standards
- Follow the existing code structure and style in the project
- Use clear, descriptive variable and function names
- Add comments to explain complex logic
- Ensure code is well-formatted and readable

### Pull Request Guidelines
- Provide a clear description of the changes in your pull request
- Include the purpose and context of your changes
- Reference any related issues in the pull request description

### Issue Reporting
- Use the GitHub Issues section to report bugs or suggest improvements
- Provide detailed information, including steps to reproduce for bug reports
- Include relevant context, error messages, or screenshots when applicable

*Note: By contributing to this project, you agree to abide by the project's Code of Conduct and licensing terms.*

## License

This project is licensed under the MIT License. For the full license text, please see the [LICENSE](LICENSE) file in the repository.

The MIT License is a permissive open-source license that allows you to:
- Use the software commercially
- Modify the software
- Distribute the software
- Use the software privately
- Place a warranty on the software

The only condition is that you include the original copyright notice and the permission notice in any substantial portion of the software.