# Config library

This is a library to get configuration from env variables, toml file or default config.

## Example how to use it
```
package main

import (
	"fmt"

	configLibrary "github.com/hermeznetwork/config-library"
)

func main() {
    path := "./config.toml"
    defaultValues := `
    ConfVariable1 = "string"
    ConfVariable2 = false
    ConfVariable3 = 1
    `
    type model struct {
        ConfVariable1 string `env:"PREFIX_CONFVARIABLE1"`
        ConfVariable2 bool   `env:"PREFIX_CONFVARIABLE2"`
        ConfVariable3 int    `env:"PREFIX_CONFVARIABLE3"`
    }
	var cfg model
	err := configLibrary.LoadConfig(path, defaultValues, &cfg)
	if err != nil {
        //Handle error
        fmt.Println(err)
    }
    fmt.Println("Configuration: ", cfg)
}
```
#### Priority:
1. Env variables
2. Configuration file (toml)
3. default configuration values

This library allows to use different priorities in order to fill the cfg variable that contains the configuration.
Env variables have the highest priority and will overwrite any other configuration. If Env variables are not setted,
the configuration file will be used. At the end, if there is no configuration setted, the application will run using
the default configuration values.