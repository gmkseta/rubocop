# Versioning

!!! Note

    Some of the information here is forward looking, as RuboCop 1.0 is still not released.

RuboCop is stable between major versions, both in terms of API and cop
configuration.

## Release Policy

We're following [Semantic Versioning](http://semver.org/) (as much as
one can be following it when the major version is 0). At this point
bumps of the minor (second) version number are considered major releases
and always include new features or significant changes to existing
features. API compatibility between major releases is a big concern, as
there are many RuboCop extensions that can be affected by breaking API
changes.

The development cycle for the next major
release starts immediately after the previous one has been
shipped. Bugfix/point releases (if any) address only serious bugs and
never contain new features.

Here are a few examples:

* 0.50.0 - Feature release
* 0.50.1 - Bug-fix release
* 0.50.2 - Bug-fix release
* 0.51.0 - Feature release

## Pending Cops

In the early versions of RuboCop a common source of frustration was that
new cops were added to pretty much every release, and as they were enabled
by default, every upgrade resulted in broken CI builds and trying to figure
out what exactly was changed. After considering many options to address
this eventually we opted for an approach that limits these type of changes
to major RuboCop releases.

Now new cops introduced between major versions are set to a special pending
status and are not enabled by default. A warning is emitted if such cops
are not explicitly enabled or disabled in the user configuration. Here's
one such message:

```
The following cops were added to RuboCop, but are not configured. Please
set Enabled to either `true` or `false` in your `.rubocop.yml` file:
 - Style/HashEachMethods (0.80)
 - Style/HashTransformKeys (0.80)
 - Style/HashTransformValues (0.80)
For more information: https://docs.rubocop.org/en/latest/versioning/
```

You can see that 3 new cops were added in RuboCop 0.80 and it's up to you
to decide if you want to enable or disable them.

To suppress this message set `NewCops` to either `enable` or `disable` in your `.rubocop.yml` file.

The following setting or using `rubocop --enable-pending-cops` command-line option, pending cops are enabled in bulk.

```yaml
AllCops:
  NewCops: enable
```

The following setting or using `rubocop --disable-pending-cops` command-line option, pending cops are disabled in bulk.

```yaml
AllCops:
  NewCops: disable
```

The command-line options takes precedence over `.rubocop.yml` file.

Or set `Enabled` to either `true` or `false` in your `.rubocop.yml` file.

`Style/ANewCop` is an example of a newly added pending cop:

```yaml
Style/ANewCop:
  Enabled: true
```

or

```yaml
Style/ANewCop:
  Enabled: false
```

On major version updates, pending cops are enabled in bulk.
