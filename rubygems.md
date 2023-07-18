# require 'date' #

This is how `require 'date'` works:

```console
% ruby -v
ruby 2.6.10p210 (2022-04-12 revision 67958) [arm64-darwin21]
% ruby -e 'puts Gem::VERSION'
3.0.3.1
```

```mermaid
sequenceDiagram
  participant rubygems.rb
  activate rubygems.rb
    rubygems.rb->>Specification: load_defaults
    activate Specification
      Specification->>BasicSpecification: default_specifications_dir
      activate BasicSpecification
        BasicSpecification->>Gem: default_dir
        Gem-->>BasicSpecification: $HOME/.rbenv/versions/2.6.10/lib/ruby/gems/2.6.0
        BasicSpecification-->>Specification: $HOME/.rbenv/versions/2.6.10/lib/ruby/gems/2.6.0/specifications/default
      deactivate BasicSpecification
      loop each_spec
        loop each_gemspec
          Specification->>Util: glob_files_in_dir("*.gemspec", dir)
        end
      end
    deactivate Specification
  deactivate rubygems.rb
```
