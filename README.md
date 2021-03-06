# Versioning `fastlane` Plugin

[![CI Status](https://travis-ci.org/SiarheiFedartsou/fastlane-plugin-versioning.svg?branch=master)
[![fastlane Plugin Badge](https://rawcdn.githack.com/fastlane/fastlane/master/fastlane/assets/plugin-badge.svg)](https://rubygems.org/gems/fastlane-plugin-versioning)


## Getting Started

This project is a [fastlane](https://github.com/fastlane/fastlane) plugin. To get started with fastlane-plugin-versioning, add it to your project by running:

```bash
fastlane add_plugin versioning
```

## About versioning

Extends fastlane versioning actions. Allows to set/get versions without using agvtool and do some other small tricks.
Note that since version 0.2.6 all targets that you pass to actions like `increment_version_number_in_plist` or `get_info_plist_path` must be shared.
To make your target shared go to "Manage schemes" in Xcode and tick "Shared" checkbox near your target name.

## Actions

### increment_version_number_in_plist

Increment/set version number in Info.plist of specific target. Doesn't use agvtool (unlike default increment_version_number).

```ruby
increment_version_number_in_plist # Automatically increment patch version number.
increment_version_number_in_plist(
  bump_type: 'patch' # Automatically increment patch version number
)
increment_version_number_in_plist(
  bump_type: 'minor' # Automatically increment minor version number
)
increment_version_number_in_plist(
  bump_type: 'major' # Automatically increment major version number
)
increment_version_number_in_plist(
  version_number: '2.1.1' # Set a specific version number
)
increment_version_number_in_plist(
  # Automatically increment patch version number. Use App Store version number as a source.
  version_source: 'appstore'
)

increment_version_number_in_plist(
  # specify specific version number (optional, omitting it increments patch version number)
  version_number: '2.1.1',   
  # (optional, you must specify the path to your main Xcode project if it is not in the project root directory
  # or if you have multiple xcodeproj's in the root directory)
  xcodeproj: './path/to/MyApp.xcodeproj'  
  # (optional)
  target: 'TestTarget'
)
```

### get_version_number_from_plist

Get version number from Info.plist of specific target. Doesn't use agvtool (unlike default get_version_number).

```ruby
version = get_version_number_from_plist(xcodeproj: 'Project.xcodeproj', # optional
                                        target: 'TestTarget', # optional
                                        # optional, must be specified if you have different Info.plist build settings
                                        # for different build configurations
                                        build_configuration_name: 'Release')
```

### get_app_store_version_number


```ruby
version = get_app_store_version_number(xcodeproj: 'Project.xcodeproj', # optional
                                        target: 'TestTarget', # optional
                                        # optional, must be specified if you have different Info.plist build settings
                                        # for different build configurations
                                        build_configuration_name: 'Release')
)
version = get_app_store_version_number(bundle_id: 'com.apple.Numbers')

```

### get_version_number_from_git_branch

```ruby
# Extracts version number from git branch name.
# `pattern` is pattern by which version number will be found, `#` is place where action must find version number.
# Default value is 'release-#'(for instance for branch name 'releases/release-1.5.0' will extract '1.5.0')
version = get_version_number_from_git_branch(pattern: 'release-#')

```

### increment_build_number_in_plist

Increment/set build number in Info.plist of specific target. Doesn't use agvtool (unlike default increment_version_number).

```ruby
increment_build_number_in_plist # Automatically increments build number.
increment_build_number_in_plist(
  build_number: 42 # set build number to 42
)
```

### get_build_number_from_plist

Get build number from Info.plist of specific target. Doesn't use agvtool (unlike default get_build_number).

```ruby
version = get_build_number_from_plist(xcodeproj: "Project.xcodeproj", # optional
                                        target: 'TestTarget', # optional
                                        build_configuration_name: 'Release') # optional, must be specified if you have different Info.plist build settings for different build configurations
```


### get_info_plist_path

Get a path to target's Info.plist
```ruby
get_info_plist_path(xcodeproj: 'Test.xcodeproj', # optional
                    target: 'TestTarget', # optional
                    # optional, must be specified if you have different Info.plist build settings
                    # for different build configurations
                    build_configuration_name: 'Release')
```



## Issues and Feedback

For any other issues and feedback about this plugin, please submit it to this repository.

## Troubleshooting

For some more detailed help with plugins problems, check out the [Plugins Troubleshooting](https://github.com/fastlane/fastlane/blob/master/fastlane/docs/PluginsTroubleshooting.md) doc in the main `fastlane` repo.

## Using `fastlane` Plugins

For more information about how the `fastlane` plugin system works, check out the [Plugins documentation](https://github.com/fastlane/fastlane/blob/master/fastlane/docs/Plugins.md) in the main `fastlane` repo.

## About `fastlane`

`fastlane` automates building, testing, and releasing your app for beta and app store distributions. To learn more about `fastlane`, check out [fastlane.tools](https://fastlane.tools).
