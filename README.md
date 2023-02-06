# Bundler test repo


This was a reproducible case where `Gemfile.lock` doesn't include platform-specific gems for all gems that have them. It was fixed in [rubygems/rubygems#5743: Platform specific gems not being found by bundler](https://github.com/rubygems/rubygems/issues/5743)

Here you can see google-protobuf has the platform-specific versions, but another gem grpc does not even though it does have platform-specific versions.


## Testing

Show Gemfile.lock doesn't get platform-specific gems for grpc

```
bundle install
```

Start from scratch, and see platform-specific gems for grpc

```
rm Gemfile.lock
bundle install
bundle lock --add-platform x86_64-linux
bundle lock --add-platform x86_64-darwin-21
bundle lock --add-platform arm64-darwin-21
bundle lock --remove-platform ruby
```
