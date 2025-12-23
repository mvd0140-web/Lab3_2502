``` java
class Item {
    public double cost;
    public String status;
    public String name;
    public int amount;
    @Override
    public String toString() {
        return String.format("Название: %s | Цена: %.2f | Количество: %d | Статус: %s",
                name, cost, amount, status);
    }
    public Item (String name, double cost, int amount, String status) {
        this.name = name;
        this.cost = cost;
        this.status = status;
        this.amount = amount;
    }
    public double getCost() {
        return cost;
    }
}
```
