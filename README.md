# configlib
Dynamic config library

# Example
## Config-Class
```php
class TestConfig extends Configuration {

    /** @ignored Will not be saved */
    private string $configName = "TEST";
    private string $where = "Unknown";
    private string $who = "Unknown";
    private array $extraData = [
        "age" => -1
    ];

    public function __construct() {
        parent::__construct(__DIR__ . DIRECTORY_SEPARATOR . "test.json", 1);
    }

    public function setWhere(string $where): void {
        $this->where = $where;
    }

    public function setWho(string $who): void {
        $this->who = $who;
    }

    public function setExtraData(array $extraData): void {
        $this->extraData = $extraData;
    }

    public function getWho(): string {
        return $this->who;
    }

    public function getConfigName(): string {
        return $this->configName;
    }

    public function getWhere(): string {
        return $this->where;
    }

    public function getExtraData(): array {
        return $this->extraData;
    }
}
```

## Main 
```php
$cfg = new TestConfig();
if (!$cfg->load()) $cfg->save(); // First save with default values
var_dump($cfg->getWhere()); // Outputs: First time: Unknown | Second time: Germany
var_dump($cfg->getWho()); // Outputs: First time: Unknown | Second time: r3pt1s
var_dump($cfg->getExtraData()); // Outputs: First time: Unknown | Second time: 14
$cfg->setWhere("Germany"); // Set the value of $where to "Germany"
$cfg->setWho("r3pt1s"); // Set the value of $who to "r3pt1s"
$cfg->setExtraData(["age" => 14]); // Set the value of $extraData to ["age" => 14]
$cfg->save(); // Saves the config with the current
```
