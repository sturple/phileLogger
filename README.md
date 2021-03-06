
# Logger For Phile CMS

This is a simple plugin, which allows logging to be enabled during development and testing of other plugins.

This logger uses [katzgrau/klogger](https://packagist.org/packages/katzgrau/klogger) for operations which has one dependent [psr/log](https://packagist.org/packages/psr/log).


## Installation
### Composer
```
php composer.phar require sturple/phile-logger:dev-master
```

### Download
```
* Install [Phile](https://github.com/PhileCMS/Phile)
* Clone this https://github.com/sturple/phileLogger repo into `plugins/sturple/phileLogger/`
```


## Usage

### setup config.php

``` php
$config['plugins']['sturple\\phileLogger'] =array('active' => false);

```


### Example to be used in other plugins
``` php
$relDir = 'lib/cache/logs';
$logLevel = '{debug|info|notice|warning|error|critical|alert|emergency}'
$options = array('extension'      => 'txt',
		 'dateFormat'     => 'Y-m-d G:i:s.u',
		 'filename'       => false,
		 'flushFrequency' => false,
	 	 'prefix'         => 'log_',
		 'logFormat'      => false,
		 'appendContext'  => true);
		 


$logger = (new \Phile\Plugin\Sturple\PhileLogger\Plugin($relDir='lib/cache/logs',
							$logLevel='debug',
							$options=array()))->getLogger();
$logger->info('You can use functions debug, info, notice, warning, error, critical, alert.');
$logger->warning('You can add arrays',array('phile'=>'CMS'));
```
#### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| dateFormat | 'Y-m-d G:i:s.u' | The format of the date in the start of the log lone (php formatted) |
| extension | 'txt' | The log file extension |
| filename | [prefix][date].[extension] | Set the filename for the log file. **This overrides the prefix and extention options.** |
| flushFrequency | `false` (disabled) | How many lines to flush the output buffer after |
| prefix  | 'log_' | The log file prefix |
| logFormat | `false` | Format of log entries |
| appendContext | `true` | When `false`, don't append context to log entries |


## Log Formatting

The `logFormat` option lets you define what each line should look like and can contain parameters representing the date, message, etc.

When a string is provided, it will be parsed for variables wrapped in braces (`{` and `}`) and replace them with the appropriate value:

| Parameter | Description |
| --------- | ----------- |
| date | Current date (uses `dateFormat` option) |
| level | The PSR log level |
| level-padding | The whitespace needed to make this log level line up visually with other log levels in the log file |
| priority | Integer value for log level (see `$logLevels`) |
| message | The message being logged |
| context | JSON-encoded context |
