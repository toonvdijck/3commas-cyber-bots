# 3Commas Bot Helpers

## Overview

This project is a collection of Python scripts designed to assist with cryptocurrency trading on the 3Commas platform. These scripts provide various functionalities, including automating trading strategies, managing bot settings, and integrating with external data sources like LunarCrush and CoinMarketCap. The goal of this project is to offer a suite of tools that can help users enhance their trading experience on 3Commas.

## Features

This project includes a variety of scripts, each designed for a specific purpose:

*   **`altrank.py`**: Updates 3Commas bot pairs based on LunarCrush AltRank™ scores.
*   **`botassistexplorer.py`**: Explores and interacts with BotAssist functionalities (assumption based on name).
*   **`coinmarketcap.py`**: Updates 3Commas bot pairs based on CoinMarketCap rankings.
*   **`compound.py`**: Manages compounding features for 3Commas bots (assumption based on name).
*   **`dealcluster.py`**: Clusters or groups deals based on certain criteria (assumption based on name).
*   **`galaxyscore.py`**: Updates 3Commas bot pairs based on LunarCrush Galaxy Score™.
*   **`tpincrement.py`**: Incrementally adjusts take-profit levels for deals (assumption based on name).
*   **`trailingstoploss.py`**: Implements a trailing stop-loss mechanism for 3Commas deals.
*   **`trailingstoploss_tp.py`**: Implements a trailing stop-loss and take-profit mechanism for 3Commas deals.
*   **`watchlist.py`**: Manages a watchlist of trading pairs for 3Commas bots.
*   **`watchlist_100eyes.py`**: Manages a watchlist based on signals from 100eyes scanner (assumption based on name and common crypto tool).

More details on the specific configuration and operation of each script can be found within their respective `.ini` files and source code.

## Setup and Configuration

### Dependencies

Most of these scripts rely on Python 3 and a set of common libraries. You can install the necessary dependencies using pip and the `requirements.txt` file:

```bash
pip install -r requirements.txt
```

### Configuration

Each bot script typically uses an `.ini` configuration file located in its data directory (usually the same directory as the script, or specified with the `-d` or `--datadir` argument).

**General Configuration Steps:**

1.  **Copy Example Configuration:** When a script is run for the first time, it will usually create an example `.ini` file (e.g., `altrank.ini`) if one doesn't exist.
2.  **Edit the `.ini` File:** Open the generated `.ini` file with a text editor.
3.  **API Keys:**
    *   You will need to provide your 3Commas API key and secret. These are usually set as `3c-apikey` and `3c-apisecret` in the `[settings]` section.
    *   Some scripts might require additional API keys for external services (e.g., `lc-apikey` for LunarCrush in `altrank.py`, `cmc-apikey` for CoinMarketCap in `coinmarketcap.py`).
4.  **Bot IDs:**
    *   Specify the 3Commas Bot ID(s) you want the script to manage. This is often a list under `botids` in the script-specific section or `[settings]`.
5.  **Other Parameters:**
    *   Review and adjust other script-specific parameters such as `timezone`, `timeinterval`, `numberofpairs`, `maxaltrankscore`, `activation-percentage`, etc., according to your needs.
    *   Detailed explanations for each parameter are usually provided as comments within the example `.ini` file or can be inferred from the script's source code.

**Example `[settings]` block (common across many scripts):**

```ini
[settings]
timezone = Europe/Amsterdam
timeinterval = 3600
debug = False
logrotate = 7
3c-apikey = Your 3Commas API Key
3c-apisecret = Your 3Commas API Secret
notifications = False
notify-urls = ["notify-url1"]
```

**Note:** Always ensure your API keys are kept confidential and secure. Do not commit them directly into your version control history if you are managing this project with Git.

## Usage

### Running the Bots

Once configured, you can run the individual bot scripts directly using Python:

```bash
python3 altrank.py
python3 coinmarketcap.py
# etc.
```

### Command-Line Arguments

Some scripts support command-line arguments to specify operational parameters:

*   `-d` or `--datadir`: Specifies the directory to use for configuration (`.ini`) and log files. If not provided, it usually defaults to the current working directory.
*   `-b` or `--blacklist`: Allows you to specify a local blacklist file to use instead of the one from 3Commas (supported by some scripts like `altrank.py` and `coinmarketcap.py`).

Example:

```bash
python3 altrank.py --datadir /path/to/your/configs --blacklist myblacklist.txt
```

Always check the specific script's source code or run it with `-h` or `--help` (if implemented) to see available command-line options.

### Docker Deployment

This project also includes support for Docker, allowing you to run the bots in containerized environments.

*   A `Dockerfile` and `docker-compose.yml` are provided in the `docker/` directory.
*   Refer to the `docker/README.md` file for detailed instructions on building and running the bots using Docker.
This can be particularly useful for deploying the bots on a server or a Raspberry Pi (a `Dockerfile.pi` is also available).

### Service Scripts

The `scripts/` directory contains example service files (e.g., for `systemd` on Linux). These can be used to run the bots as background services, ensuring they restart automatically. You may need to customize these service files to match your specific paths and user configurations.

## Contributing

Contributions to this project are welcome! If you have improvements, bug fixes, or new bot scripts that you'd like to share, please consider contributing.

**General Contribution Guidelines:**

1.  **Fork the Repository:** Start by forking the main repository to your own GitHub account.
2.  **Create a New Branch:** For each new feature or bug fix, create a new branch in your fork. This helps keep your changes organized.
    ```bash
    git checkout -b your-feature-branch
    ```
3.  **Make Your Changes:** Implement your changes, ensuring your code is clear, commented where necessary, and follows the general style of the existing project.
4.  **Test Your Changes:** If applicable, test your script thoroughly to ensure it works as expected.
5.  **Update Documentation:** If you are adding a new script or significantly changing an existing one, please update this README or other relevant documentation.
6.  **Commit Your Changes:** Commit your changes with a clear and descriptive commit message.
    ```bash
    git commit -am "Add new feature: Describe your feature"
    ```
7.  **Push to Your Fork:** Push your changes to your forked repository.
    ```bash
    git push origin your-feature-branch
    ```
8.  **Submit a Pull Request:** Open a pull request from your feature branch to the main project's `master` or `main` branch. Provide a clear description of the changes you've made.

The project maintainers will review your pull request and may suggest changes or ask for more information.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for full license text.
