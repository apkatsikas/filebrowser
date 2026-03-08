fix/surface-config-parse-errors

Fix config parse errors not being properly surfaced

Use errors.As instead of errors.Is to correctly detect
viper.ConfigParseError and return it instead of masking it
as "no config being used".

PR Title
Fix config parse errors not being surfaced correctly

When the configuration file was malformed, the application would
incorrectly report that no configuration was being used.

This happened because the error check used errors.Is instead of
errors.As, which prevented viper.ConfigParseError from being
properly detected.

This change fixes the error detection so configuration parsing
errors are correctly surfaced to the user.
