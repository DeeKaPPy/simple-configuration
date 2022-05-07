# Simple Configuration
A simple json configuration system built with [gson](https://github.com/google/gson).

## Setup 💻
### Using Maven
**REPOSITORY**
```xml
<repositories>
    <repository>
        <id>jitpack.io</id>
        <url>https://jitpack.io</url>
    </repository>
</repositories>
```

**DEPENDENCY**
```xml
<dependency>
    <groupId>com.github.User</groupId>
    <artifactId>Repo</artifactId>
    <version>1.0-SNAPSHOT</version> <!-- or replace with newer version -->
</dependency>
```

## Usage 📚
### Initialize

```java
import com.google.gson.GsonBuilder;

class Bootstrap {

    private final ConfigLoader configLoader;

    public Bootstrap() {

        configLoader = new ConfigLoader(); // you can add you own gson instance

        /*
        loading
         */
        Config config = configLoader.load(Config.class, new Config()); // pass the class and default options

        config.setName("John");

        /*
        save
         */
        configLoader.save(Config.class, config); // pass the class and the config object

        /*
        add custom adapters
         */
        configLoader.addAdapter(NewAdapter.class, new NewAdapter());
        
        /*
        add any other custom properties to GsonBuilder
         */
        GsonBuilder gsonBuilder = configLoader.getGsonBuilder(); // get the gson builder
        gsonBuilder.registerTypeAdapter(ExampleAdapter.class, new ExampleAdapter());
        gsonBuilder.excludeFieldsWithoutExposeAnnotation();
        
        configLoader.setGsonBuilder(gsonBuilder); // re set the gson builder
    }

}
```

### Config Class
```java
@ConfigurationFile(
    directory = "./configs/test",
    name = "config.json"
)
class Config {
    private String name;
    @ConfigurationExclusion
    private int age;
}
```