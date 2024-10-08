﻿# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).



## Version [4.1.0] - 2024-08-29 🚀

### Added ✨

- RCLONE_LOGS: Environment variable to disable the rclone process logging when value is set to OFF; Default is ON 📝
- RCLONE_DIR: Environment variable to set the rclone directory; Default is /data 📁

### Fixed 🛠️

- [Issue #36](https://github.com/I-am-PUID-0/DMB/issues/36) Setting RCLONE_LOG_LEVEL=OFF causes the rclone process to fail 🐛
- [Issue #37](https://github.com/I-am-PUID-0/DMB/issues/37) Error when PUID/PGID are set without values: PGID= 🐛
- [Issue #38](https://github.com/I-am-PUID-0/DMB/issues/38) Recursive chown of /data throws errors if the mount is still present 🐛
- [Issue #39](https://github.com/I-am-PUID-0/DMB/issues/39) Make rclone mount base path a variable - /data --> /user-defined ✨
- [Issue #41](https://github.com/I-am-PUID-0/DMB/issues/41) Add healthcheck for PostgreSQL process ✨
- [Issue #42](https://github.com/I-am-PUID-0/DMB/issues/42) Add clean shutdown for PostgreSQL server ✨


## Version [4.0.0] - 2024-08-28 🚀

### Breaking Changes ⚠️

- Riven: Riven backend no longer supports sqlite as a database option; PostgreSQL is now the only supported database option 📉
- PostgreSQL: To ensure the database files are persisted, a volume must be mounted to /postgres_data 📂

### Added ✨

- PUID & PGID: Environment variables to set the user and group IDs for the DMB container; Default is 1001 🆔
- POSTGRES_DATA: Environment variable to set the path for the PostgreSQL database files; Default is /postgres_data 📁
- POSTGRES_PASSWORD: Environment variable to set the password for the PostgreSQL database; Default is postgres 🔐
- POSTGRES_USER: Environment variable to set the user for the PostgreSQL database; Default is postgres 👤
- POSTGRES_DB: Environment variable to set the database name for the PostgreSQL database; Default is riven 🗄️

### Changed 🔄

- Riven: Riven backend now uses PostgreSQL as the database option; Default is postgresql+psycopg2://postgres:postgres@127.0.0.1/riven 🔧
- Riven: Riven frontend now uses PostgreSQL as the database option; Default is postgres://postgres:postgres@127.0.0.1/riven 🔄

### Fixed 🛠️

- [Issue #8](https://github.com/I-am-PUID-0/DMB/issues/8) Add support for PUID/GUID ✨
- [Issue #34](https://github.com/I-am-PUID-0/DMB/issues/34) Add PostgreSQL option for Riven backend ✨
- [Issue #35](https://github.com/I-am-PUID-0/DMB/issues/35) Riven frontend not properly connecting to the database 🐛

### Notes 📝📌

- If the Riven backend shows errors related to the database or alembic, then the Riven data directory may need to be deleted before starting the new version of Riven w/ PostgreSQL 🗑️ - backup your settings.json before deleting the data directory 📂


## Version [3.5.0] - 2024-08-08 🚀

### Added ✨

- Suppress Logs: If the LOG_LEVEL for a process is set to OFF, then logs will be suppressed for the process 🤫
- Riven Frontend: Added the latest version of the Riven frontend to the Dockerfile for image build 📦 

### Notes 📝

- The DMB image is built nightly and will include the latest version of the Riven frontend at the time of build 🌙


## Version [3.4.0] - 2024-08-05 🚀


### Fixed 🛠️

- [Issue #27](https://github.com/I-am-PUID-0/DMB/issues/27) DATABASE_URL was not being set correctly for the Riven frontend 🐛
- healthcheck: Fixed healthcheck to properly check for Riven frontend setup completion 🩺

### Changed 🔄

- Riven setup: Refactored backend and frontend setup to use ProcessHandler for consistent logging 🔄

### Added ✨

- [Issue #9](https://github.com/I-am-PUID-0/DMB/issues/9) Obfuscate sensitive data in logs
- Riven backend: UPDATERS_PLEX_ADDRESS linked to PLEX_ADDRESS 🔄
- Riven backend: UPDATERS_PLEX_TOKEN linked to PLEX_TOKEN 🔄


## Version [3.3.2] - 2024-08-03 🚀

### Fixed 🛠️

- [Issue #27](https://github.com/I-am-PUID-0/DMB/issues/27) Riven frontend needed a database connection to function properly 🐛

### Added ✨

- RIVEN_DATABASE_URL: Environment variable to set the Riven frontend database URL; Default is sqlite:////riven/backend/data/media.db 🗃️

### Changed 🔄

- GITHUB_TOKEN: Can be added to the environment variables to allow for repository downloads without rate limits 🔄


## Version [3.3.1] - 2024-08-01 🚀

### Fixed 🛠️

- healthcheck: Reverted healthcheck, for now 🐛


## Version [3.3.0] - 2024-08-01 🚀

### Fixed 🛠️

- [Issue #23](https://github.com/I-am-PUID-0/DMB/issues/23) Processes not properly killed during automatic updates 🐛
- [Issue #24](https://github.com/I-am-PUID-0/DMB/issues/24) Riven automatic update extracts to wrong directory 🐛
- [Issue #25](https://github.com/I-am-PUID-0/DMB/issues/25) Automatic update initiates update check multiple times for each instance 🐛
- [Issue #26](https://github.com/I-am-PUID-0/DMB/issues/26) Riven Frontend breaking change requires DIALECT=sqlite env variable 🐛

### Added ✨

- Automatic Update: Enabled automatic updates for Riven branches - expands automatic updates to include branches 🔄
- RIVEN_FRONTEND_DIALECT: Environment variable to set the Riven frontend database dialect; Default is sqlite - not required to be set in default configuration 🗃️
- Riven Frontend: Set npm max_old_space_size to 2048MB for Riven frontend build process - limits resource usage 📦
- Riven Frontend: Set vite minification to false for Riven frontend build process - speeds up build process and reduces resource usage 📦

### Changed 🔄

- healthcheck: Waits for Riven frontend setup to complete 🩺


## Version [3.2.0] - 2024-07-30 🚀

### Changed 🔄

- Update process: Refactored update process to apply updates to Zurg and Riven before starting the processes 🔄
- Zurg: Disabling plex_update.sh in config file has been disbaled, for now. Comment out the line in the config file to disable the Zurg based plex update process if desired 🔄

### Added ✨

- Zurg: Allow nightly release custom versions for ZURG_VERSION
- Zurg: Add plex_update.sh from Zurg to working directory for Zurg use 📦

### Fixed 🛠️

- Logging: Fixed logging for Zurg to ensure log levels are properly set 📝


## Version [3.1.0] - 2024-07-26 🚀

### Added ✨

- Shutdown: Added a shutdown function to gracefully stop the DMB container; e.g., unmount the rclone mounts 🛑


## Version [3.0.0] - 2024-07-26 🚀

### Breaking Changes ⚠️

- BACKEND_URL: Environment variable has been changed to RIVEN_BACKEND_URL to better reflect the environment variable's purpose; please update your compose file accordingly

### Added ✨

- Ratelimit for GitHub API requests ⏳
- Retries for GitHub API requests 🔄

### Fixed 🛠️

- RIVEN_ENABLED: Environment variable has been fixed to correctly enable the Riven backend and frontend; Default is false 🤞
- RIVEN_UPDATE: Environment variable has been fixed to correctly update the Riven backend and frontend; Default is false 🤞
- RIVEN_BACKEND_UPDATE: Environment variable has been fixed to correctly update the Riven backend; Default is false 🤞
- RIVEN_FRONTEND_UPDATE: Environment variable has been fixed to correctly update the Riven frontend; Default is false 🤞
- RIVEN_DATABASE_HOST: Environment variable has been fixed to correctly set the Riven database host; Default is sqlite:////riven/backend/data/media.db 🗃️
- [Issue #22](https://github.com/I-am-PUID-0/DMB/issues/22) 🐛

### Notes 📝

- BACKEND_URL has been changed to RIVEN_BACKEND_URL. The value is automatically set when the variable is not enabled. The default value is http://127.0.0.1:8080 🌐
- RIVEN_DATABASE_HOST value is automatically set when the variable is not enabled. The default value is sqlite:////riven/backend/data/media.db 🗃️



## Version [2.0.0] - 2024-07-25

### Breaking Changes

- Riven: Directory structure has changed to allow for split riven instances - backend and frontend - please update your compose file volumes accordingly
- RIVEN_BRANCH: Is now split into RIVEN_FRONTEND_BRANCH and RIVEN_BACKEND_BRANCH
- RIVEN_ENABLED: Environment variable will enable the Riven backend and frontend without the need to set the RIVEN_FRONTEND_ENABLED and RIVEN_BACKEND_ENABLED variables
- RIVEN_UPDATE: Environment variable to update the Riven backend and frontend; Default is false

### Added

- RIVEN_BACKEND_ENABLED: Environment variable to enable the Riven backend; Default is false
- RIVEN_FRONTEND_ENABLED: Environment variable to enable the Riven frontend; Default is false
- RIVEN_BACKEND_BRANCH: Environment variable to set the Riven backend branch; Default is main
- RIVEN_FRONTEND_BRANCH: Environment variable to set the Riven frontend branch; Default is main
- RIVEN_BACKEND_UPDATE: Environment variable to update the Riven backend; Default is false
- RIVEN_FRONTEND_UPDATE: Environment variable to update the Riven frontend; Default is false
- RIVEN_BACKEND_VERSION: Environment variable to set the Riven backend version; Default is latest
- RIVEN_FRONTEND_VERSION: Environment variable to set the Riven frontend version; Default is latest
- BACKEND_URL: Environment variable to set the Riven backend URL; Default is http://127.0.0.1:8080
- RIVEN_DATABASE_HOST: Environment variable to set the Riven database host; Default is sqlite:////riven/backend/data/media.db
- COLOR_LOG_ENABLED: Environment variable to enable color logging; Default is false
- ffmpeg: Added ffmpeg to the Dockerfile for Zurg use of ffprobe to extract media information from files, enhancing media metadata accuracy.


### Notes

- **Delete all Riven files and directories within the data directory before starting the new version of Riven!**
- **Automatic updates for Riven backend and frontend are not funtioal yet; will be fixed in a follow-on release.**
- **Other features may also not be functional yet; will be fixed in a follow-on release.**
- This release resolves [Issue #19](https://github.com/I-am-PUID-0/DMB/issues/19), [Issue #20](https://github.com/I-am-PUID-0/DMB/issues/20), and [Issue #10](https://github.com/I-am-PUID-0/DMB/issues/10)



## Version [1.2.0] - 2024-07-19

### Added

- [Issue #18](https://github.com/I-am-PUID-0/DMB/issues/18): Added DMB_LOG_SIZE environment variable to set the maximum size of the log file; Default is 10MB


## Version [1.1.0] - 2024-07-17

### Changed

- Rclone: WebDAV URL check for Zurg startup processes accepts any 200 status code as a valid response
- DMB: Refactored to use common functions under utils 


## Version [1.0.3] - 2024-07-16

### Fixed

- Rclone: Fixed WebDAV URL check for Zurg startup processes when Zurg user and password are set in config.yml


## Version [1.0.2] - 2024-07-16

### Fixed

- Zurg: Fixed the removal of Zurg user and password if previously set in config.yml


## Version [1.0.1] - 2024-07-16

### Fixed

- DMB: Introduced a Riven startup check for the symlinked directory to ensure the Zurg startup processes have finished before starting Riven
- DMB: Introduced a Rclone startup check for the Zurg WebDAV URL to ensure the Zurg startup processes have finished before starting Rclone


## Version [1.0.0] - 2024-06-25

### Breaking Changes

- DMB: Updated PDZURG_LOG_LEVEL to DMB_LOG_LEVEL
- DMB: Updated PDZURG_LOG_COUNT to DMB_LOG_COUNT

### Changed

- [Issue #5](https://github.com/I-am-PUID-0/DMB/issues/5): Added initial sleep time to allow for services to start
- [Issue #6](https://github.com/I-am-PUID-0/DMB/issues/6): Disabled Zurg plex_update.sh - not needed
- [Issue #7](https://github.com/I-am-PUID-0/DMB/issues/7): Cleanup Riven logging

### Added

- [Issue #1](https://github.com/I-am-PUID-0/DMB/issues/1): All Riven settings now assignable with environment variables
- Riven: RIVEN_LOG_LEVEL environment variable - Riven log level is only configurable to DEBUG or INFO; Default is INFO

### Removed

- [Issue #3](https://github.com/I-am-PUID-0/DMB/issues/3): Removed Jellyfin environment variables
- [Issue #2](https://github.com/I-am-PUID-0/DMB/issues/2): Removed PLEX_REFRESH environment variable


## Version [0.2.0] - 2024-06-22

### Added

- Zurg: GITHUB_TOKEN environment variable to use for access to the private sponsored zurg repository

### Removed

- Zurg: PLEX_REFRESH environment variable
- Zurg: PLEX_MOUNT environment variable


## Version [0.1.0] - 2024-06-22

### Added

- Riven: RIVEN_BRANCH environment variable to select the branch to use for the riven repository

### Fixed

- rclone: Fixed rclone process w/ Riven
- Healthcheck: Fixed healthcheck process w/ Riven


## Version [0.0.1] - 2024-06-21

### Added

- Initial Push