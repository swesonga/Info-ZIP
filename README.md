# retry-zip

retry-zip is a simple modification of [Info-ZIP](http://www.info-zip.org/) to support retrying failed I/O operations.
This change was motivated by intermittent failures when building the OpenJDK on Microsoft Windows (specifically in the Cygwin environment).
Such failures occurred when zip files could not be opened (because they were still being updated).
Instead of failing the build, retry-zip enables the operations to be retried after a specified delay.
The number of retries is also customizable.

## New Command-line Options

`--io-max-retries`
Specifies the maximum number of I/O operation attempts after the initial attempt fails. Defaults to 0 if not specified (to keep the original behavior of Info-ZIP).

`--io-retry-delay`
Specifies the number of seconds to wait between retry attempts. Defaults to 30 seconds if not specified.

## Notes
When an operation fails and needs to be retried, debug information is also displayed for the remainder of the application's execution.
This is exactly the same diagnostic information displayed when the `-sd` option is passed in to the zip application.
