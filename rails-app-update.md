# rails app:update #

This is how `rails app:update` works:

```console
% ruby -v
ruby 2.6.10p210 (2022-04-12 revision 67958) [arm64-darwin21]
% rails app:update
```

## bin/rails ##

```sh
#!/usr/bin/env ruby
APP_PATH = File.expand_path('../config/application', __dir__)
require_relative '../config/boot'
require 'rails/commands'
```

## require 'rails/commands' ##

```mermaid
sequenceDiagram
  participant bin/rails
  activate bin/rails
    bin/rails->>commands.rb: 
    commands.rb->>Command: invoke(command = "app:update", ARGV = [])
    activate Command
      Command->>Command: find_by_namespace("app", "update")
      Note over Command: At first, do nothing
      Command->>Command: find_by_namespace("rake")
      activate Command
        Command->>Command: lookup(['rake', 'rails:rake'])
        Command->>Command: namespace_to_paths(namespaces)
        Activate Command
          Command-->>Command: 
        deactivate Command
      deactivate Command
      Command->>RakeCommand: perform(task = 'app:update', *)
      activate RakeCommand
        RakeCommand->>RakeCommand: require_rake
        RakeCommand->>Rake: application
        activate Rake
          Rake->>Application: new
          activate Application
            Application->>TaskManager: initialize
          deactivate Application
        deactivate Rake
      deactivate RakeCommand
    deactivate Command
  deactivate bin/rails
```
