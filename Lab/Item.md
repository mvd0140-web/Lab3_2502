``` java
class Item {
    public double cost; // Стоимость товара
    public String status; // Статус куплено/не куплено
    public String name; // Название товара
    public int amount; // Количество товара
    @Override
    // Вывод товара в строковом формате
    public String toString() {
        return String.format("Название: %s | Цена: %.2f | Количество: %d | Статус: %s",
                name, cost, amount, status);
    }
    // Создание нового товара
    public Item (String name, double cost, int amount, String status) {
        this.name = name;
        this.cost = cost;
        this.status = status;
        this.amount = amount;
    }
    // Функция, возвращающая стоимость товара
    public double getCost() {
        return cost;
    }
}
```
