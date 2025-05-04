# ClickBot: Advanced Multi-Monitor UI Automation Tool

## Project Overview

ClickBot is an intelligent, automated UI interaction tool designed to streamline repetitive screen interactions through advanced image matching and error recovery techniques. The primary purpose of this application is to provide a robust, configurable bot that can automatically detect and interact with specific UI elements across multiple monitor configurations.

### Key Features
- **Adaptive Monitor Detection**: Automatically identifies and tracks the target application window across multiple monitors
- **Intelligent Image Matching**: Uses advanced template matching with configurable confidence thresholds
- **Error Recovery**: Implements sophisticated error detection and recovery mechanisms
- **Flexible Configuration**: Supports customizable scan intervals, confidence levels, and debug modes

### Core Capabilities
- Automated UI element detection using image template matching
- Precision screen scanning with adjustable confidence thresholds
- Automatic click interactions based on matched UI elements
- Comprehensive logging and debug support
- Graceful error handling and recovery
- Multi-monitor support with dynamic screen detection

### Benefits
- Reduces manual repetitive UI interactions
- Increases automation efficiency for complex screen-based tasks
- Provides robust error handling and recovery
- Offers extensive configurability for different use cases
- Supports debugging and detailed logging for troubleshooting

## Getting Started, Installation, and Setup

### Prerequisites

- Python 3.8 or higher
- Git
- A working development environment with Python and pip

### System Requirements

- Operating System: Linux (tested), macOS, or Windows
- Monitors: Multi-monitor support available
- Cursor AI integration

### Installation Steps

1. Clone the repository:
```bash
git clone https://github.com/yourusername/cursor-auto-accept.git
cd cursor-auto-accept
```

2. Run the setup script to prepare the environment:
```bash
./setup.sh
```

The setup script will:
- Create necessary directories
- Set up file permissions
- Create a Python virtual environment
- Install required dependencies

### Dependencies

The project requires the following Python packages (automatically installed by setup):
- opencv-python (>=4.8.0)
- numpy (>=1.24.0)
- pyautogui (>=0.9.54)
- pillow (>=10.0.0)
- mss (>=9.0.1)

### Calibration Process

Before first use, calibrate the bot for each monitor:

1. Stop any running bot instances:
```bash
./stop_clickbot.sh
```

2. Run calibration for all monitors:
```bash
source venv/bin/activate
python cursor_auto_accept.py --capture
```

Or calibrate a specific monitor:
```bash
python cursor_auto_accept.py --capture --monitor 0  # First monitor
python cursor_auto_accept.py --capture --monitor 1  # Second monitor
```

#### Calibration Steps
- Move Cursor to the target monitor
- Trigger an AI prompt
- Move mouse over the accept button
- Keep mouse still for 5 seconds
- Wait for confirmation message
- Press Enter to continue to next monitor (if calibrating multiple)

### Running the Application

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

To run the application directly in development mode:
```bash
source venv/bin/activate
python cursor_auto_accept.py
```

### Troubleshooting

- Ensure Python virtual environment is activated
- Check `temp/logs/clickbot.log` for detailed error messages
- Verify monitor-specific calibration images in `assets/` directory

## Usage

The Cursor Auto Accept tool provides a command-line interface with several key options for managing the auto-accept functionality.

### Basic Operation

Start the bot using the main script:

```bash
python cursor_auto_accept.py
```

This launches the control window that allows you to start, stop, and calibrate the bot.

### Command-Line Options

#### Calibration
Calibrate the bot for a specific monitor or all monitors:

```bash
# Calibrate all monitors
python cursor_auto_accept.py --capture

# Calibrate a specific monitor (0-based index)
python cursor_auto_accept.py --capture --monitor 0
```

During calibration, you'll be guided to:
- Move your cursor over the AI accept button
- Keep the cursor still for 5 seconds
- Allow the tool to capture the button's appearance

#### Test Mode
Run the bot in test mode with a 10-second timeout:

```bash
python cursor_auto_accept.py --test
```

### Interactive Control Window

The bot provides a graphical control window with these key features:

- **Play/Pause Button (▶/⏸)**: Start or stop the auto-accept functionality
- **Gear Button (⚙)**: Initiate calibration process
- **Status Display**: Shows current bot state (Ready, Running, Calibrating)
- **Log Window**: Displays detailed bot activity and debugging information

### Example Workflow

1. First-time setup:
```bash
# Calibrate for the first monitor
python cursor_auto_accept.py --capture
```

2. Start the bot:
```bash
python cursor_auto_accept.py
```
- Click the play button (▶) in the control window
- The bot will begin automatically accepting AI suggestions

3. Stop the bot:
- Click the pause button (⏸) in the control window

### Monitoring

Logs are automatically saved to `temp/logs/clickbot.log`. You can monitor live logs with:

```bash
tail -f temp/logs/clickbot.log
```

### Notes

- The bot is rate-limited to 8 clicks per minute
- Calibration is monitor-specific
- The tool automatically restores your cursor position after clicking

## Command Reference

### Command Line Options

| Option | Description | Default | Usage Example |
|--------|-------------|---------|--------------|
| `--capture` | Initiate recalibration by capturing new accept button images | Disabled | `python cursor_auto_accept.py --capture` |
| `--monitor` | Specify a particular monitor for calibration (0-based index) | All monitors | `python cursor_auto_accept.py --capture --monitor 0` |
| `--test` | Run in test mode with a 10-second timeout | Disabled | `python cursor_auto_accept.py --test` |

### Available Scripts

| Script | Purpose | Usage |
|--------|---------|-------|
| `start_clickbot.sh` | Start the Cursor Auto Accept bot | `./start_clickbot.sh` |
| `stop_clickbot.sh` | Stop the running bot | `./stop_clickbot.sh` |
| `setup.sh` | Set up project environment and dependencies | `./setup.sh` |

### Flags and Arguments Details

#### `--capture`
- Triggers the calibration mode for capturing accept button images
- Captures button images for one or all monitors
- Requires user interaction to hover over and click accept buttons
- Generates monitor-specific button templates in `assets/monitor_X/` directory

#### `--monitor`
- Select a specific monitor by its index when calibrating
- Indexes are 0-based (0 for first monitor, 1 for second, etc.)
- Allows targeted calibration for multi-monitor setups
- If not specified, defaults to calibrating the first available monitor

#### `--test`
- Runs the bot in a limited test mode
- Automatically exits after 10 seconds
- Useful for quick verification of bot functionality
- Does not perform actual accept button interactions

### Runtime Limitations
- Maximum 8 clicks per minute (rate-limited)
- Requires pre-calibration before first use
- Supports single-monitor configuration by default

## Configuration

The project supports configuration through several methods:

### Plugin Configuration

The project includes a `cursor-plugin.json` configuration file with the following key settings:

```json
{
    "cursorAutoAccept.enabled": true
}
```

- `cursorAutoAccept.enabled`: A boolean flag to enable or disable automatic prompt acceptance
  - Default: `true`
  - Type: Boolean

### Logging Configuration

Logging can be configured programmatically using the `setup_logging()` function in `logging_config.py`. Key configuration options include:

- Log Level: Controlled by the `debug_mode` parameter
  - `False` (default): Sets logging to INFO level
  - `True`: Sets logging to DEBUG level
- Log File Location: Automatically created in a `logs` directory
- Log File Rotation:
  - Maximum file size: 10MB
  - Backup log files: Up to 5 previous logs are retained

### Customization Options

- Log files are generated with detailed naming: `{component_name}.log`
- Supports both file and console logging
- Flexible logging with different formatters for file and console output

#### Example Logging Setup

```python
logger = setup_logging('your_component_name', debug_mode=False)
```

### Configuration Best Practices

- Place configuration files in the root project directory
- Ensure proper permissions for log file creation
- Adjust debug mode based on your development or production needs

## Technologies Used

### Programming Language
- Python 3.x

### Core Libraries and Frameworks
- NumPy: Numerical computing and array operations
- OpenCV (opencv-python): Image processing and computer vision
- Pillow (PIL): Image manipulation and handling
- PyAutoGUI: Cross-platform GUI automation

### System and Utility Libraries
- OS: Operating system interactions
- Sys: System-specific parameters and functions
- Signal: Signal handling for process management
- Argparse: Command-line argument parsing
- Time: Time-related functions
- Datetime: Date and time manipulation

### Monitoring and Automation Tools
- MSS: Cross-platform screen capture library

### Development and Debugging
- Logging: Built-in Python logging for application monitoring
- pytest (implied by test files): Unit testing framework

### Platform Compatibility
- Cross-platform (Windows, macOS, Linux) support through Python libraries

## Contributing

We welcome contributions to the Cursor Auto Accept project! To help maintain code quality and collaboration efficiency, please follow these guidelines:

### Branch Strategy

- Create a new branch for each major feature or significant change
- Use a timestamp or descriptive name for your branch
- Commit work frequently, focusing on logical groupings of changes

### Contribution Process

1. Fork the repository
2. Create a new branch for your feature or bugfix
3. Make your changes with clear, concise commits
4. Write or update tests to cover your changes
5. Ensure all existing tests pass
6. Submit a pull request with a clear description of your changes

### Code Guidelines

- Follow Python's PEP 8 style guide
- Write clear, commented code
- Include type hints where possible
- Maintain consistent formatting

### Testing

- All new features must include corresponding unit tests
- Run existing test suite before submitting a pull request:
  ```bash
  python -m pytest test_*.py
  ```

### Reporting Issues

- Use GitHub Issues to report bugs or suggest enhancements
- Include detailed information:
  - Description of the issue
  - Steps to reproduce
  - Expected vs. actual behavior
  - Python version
  - Operating system details

### Development Setup

1. Clone the repository
2. Create a virtual environment
3. Install development dependencies:
   ```bash
   python -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```

### Code of Conduct

- Be respectful and inclusive
- Provide constructive feedback
- Collaborate openly and professionally

Thank you for contributing to Cursor Auto Accept!

## License

This project is licensed under the [MIT License](LICENSE). 

#### Key Permissions
- Commercial use
- Modification
- Distribution
- Private use

#### Key Limitations
- Liability: Limited warranty
- No trademark rights
- No patent rights

#### Conditions
- License and copyright notice must be included with the software

For the full license details, please see the [LICENSE](LICENSE) file in the repository.