``` java
class Spisok {
    public static PrintStream out = System.out;
    public Item [] items = new Item[100]; // Массив, хранящий все товары в списке
    private int k = -1; // Переменная, отвечающая за количество товаров в списке
    @Override
    // Вывод списка товаров в стороковм формате
    public String toString() {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i <= k; i++) {
            sb.append(i + 1).append(". ").append(items[i]).append("\n");
        }
        return sb.toString();
    }
    // Функция, увеличивающая k для индексации товара в списке
    private void kolvo() {
        k++;
    }
    // Добавление нового товара в список
    public void add(String name, double cost, int amount, String status){
        kolvo();
        Item i1 = new Item(name, cost, amount, status);
        items[k] = i1;
    }
    // Функция, определяющая хватит ли бюджета для покупки того или иного товара
    public boolean dostatochno(int a, double sum) {
        double q = items[a-1].cost * items[a-1].amount;
        if (q <= sum) {
            return true;
        }
        else {
            return false;
        }
    }
    // Функция, определяющая можно ли купить товар в зависимости от статуса куплено/не куплено
    public void dostatochno1(int a, double sum) {
        if (dostatochno(a, sum) && items[a-1].status.equals("Не куплено")) {
            out.println("Можно купить");
        }
        else if (dostatochno(a, sum) && items[a-1].status.equals("Куплено")) {
            out.println("Товар уже куплен");
        }
        else {
            out.println("Нельзя купить");
        }
    }
    // Функция, реализующая покупку товара
    public double pokupka(int a, double sum) {
        if (dostatochno(a,sum) && items[a-1].status.equals("Не куплено")) {
            items[a-1].status = "Куплено";
            out.println("Куплено");
            sum -= items[a-1].cost * items[a-1].amount;
            return sum;
        }
        else if (dostatochno(a,sum) && items[a-1].status.equals("Куплено")){
            out.println("Продукт уже куплен");
            return sum;
        }
        else {
            out.println("Не хватает");
            return sum;
        }
    }
    // Функция, возвращающая подную стоимость списка
    public double polnayacost() {
        double q = 0;
        for (int i = 0; i <= k; i++) {
            q += items[i].cost * items[i].amount;
        }
        return q;
    }
    // Функция,возвращающая стоимость всех некупленных товаров
    public double fullnekupleno() {
        double q = 0;
        for (int i = 0; i <= k; i++) {
            if (items[i].status.equals("Не куплено")) {
                q += items[i].cost * items[i].amount;
            }
        }
        return q;
    }
    // Функция, позволяющая узнать, может ли пользователь при текущем бюджете купить весь список некупленных товаров
    public void kupluvse(double sum) {
        double q = fullnekupleno();
        if (q <= sum && q != 0) {
            out.println("Да!");
        }
        else if (q == 0) {
            out.println("Уже все куплено!");
        }
        else {
            out.println("Нет!");
        }
    }
    // Функция, возвращающая значение суммы, которой не хватает для покупки некупленныых товаров
    public void nehvataet(double sum) {
        double q = fullnekupleno();
        if (q <= sum && q != 0) {
            out.println("Вам хватает денег!");
        }
        else if (q == 0) {
            out.println("Уже все куплено!");
        }
        else {
            double w = q - sum;
            out.println("Вам не хватает: " + w);
        }
    }
    // Сортировка списка, начиная с дешевых товаров
    public void sorte() {
        Arrays.sort(items,0,k + 1,Comparator.comparingDouble(Item::getCost));
    }
    // Сортировка списка, начиная с дорогих товаров
    public void sortp() {
        Arrays.sort(items,0,k + 1, Comparator.comparingDouble(Item::getCost).reversed());
    }
    // Функция, возвращающая самый дорогой товар
    public void samydor() {
        double q = items[0].cost * items[0].amount;
        Item result = items[0];
        for (int i = 1; i <= k; i++) {
            if (items[i].cost * items[i].amount > q && items[i].status.equals("Не куплено")) {
                    result = items[i];
            }
            else if (items[i].cost * items[i].amount == q && items[i].status.equals("Не куплено")) {
                if (items[i].cost > items[0].cost) {
                    result = items[i];
                }
            }
        }
        if (result.status.equals("Куплено")) {
            out.println("Все товары куплены");
        }
        else {
            out.println(result);
        }
    }
    // Функция, возвращающая самый дешевый товар
    public Item samydesh() {
        double q = items[0].cost * items[0].amount;
        Item result = items[0];
        for (int i = 1; i <= k; i++) {
            if (items[i].cost * items[i].amount < q && items[i].status.equals("Не куплено")) {
                    result = items[i];
            }
            else if (items[i].cost * items[i].amount == q && items[i].status.equals("Не куплено")) {
                if (items[i].cost < items[0].cost) {
                    result = items[i];
                }
            }
        }
        return result;
    }
    // Функция, реализующая попытку купить все товары
    public double kupitVse(double budget, boolean fromCheapest) {
        Item[] sortedItems = Arrays.copyOf(items, k + 1);
        if (fromCheapest) {
            Arrays.sort(sortedItems, 0, k + 1, Comparator.comparingDouble(Item::getCost));
        } else {
            Arrays.sort(sortedItems, 0, k + 1, Comparator.comparingDouble(Item::getCost).reversed());
        }
        double remainingBudget = budget;
        int kuplenoCount = 0;
        for (int i = 0; i <= k; i++) {
            Item item = sortedItems[i];
            if (item.status.equals("Куплено")) {
                continue;
            }
            double totalCost = item.cost * item.amount;
            if (totalCost <= remainingBudget) {
                for (int j = 0; j <= k; j++) {
                    if (items[j] == item) {
                        items[j].status = "Куплено";
                        break;
                    }
                }
                remainingBudget -= totalCost;
                kuplenoCount++;
                out.println("Куплен: " + item.name + " за " + String.format("%.2f", totalCost));
            } else {
                out.println("Не удалось купить: " + item.name + " (не хватает " +
                        String.format("%.2f", totalCost - remainingBudget) + ")");
                break;
            }
        }
        out.println("Куплено товаров: " + kuplenoCount);
        out.println("Остаток бюджета: " + String.format("%.2f", remainingBudget));
        return remainingBudget;
    }
    // Функция, реализующая попытку купить определенное количество товаров
    public double kupitKolvo(double budget, int count, boolean fromCheapest) {
        if (count <= 0) {
            out.println("Количество должно быть положительным");
            return budget;
        }
        Item[] availableItems = new Item[k + 1];
        int availableCount = 0;

        for (int i = 0; i <= k; i++) {
            if (items[i] != null && items[i].status.equals("Не куплено")) {
                availableItems[availableCount] = items[i];
                availableCount++;
            }
        }
        if (availableCount == 0) {
            out.println("Все товары уже куплены!");
            return budget;
        }

        if (count > availableCount) {
            out.println("Доступно только " + availableCount + " товаров");
            count = Math.min(count, availableCount);
        }
        if (fromCheapest) {
            Arrays.sort(availableItems, 0, availableCount, Comparator.comparingDouble(Item::getCost));
        } else {
            Arrays.sort(availableItems, 0, availableCount, Comparator.comparingDouble(Item::getCost).reversed());
        }
        double remainingBudget = budget;
        int boughtCount = 0;
        for (int i = 0; i < count; i++) {
            Item item = availableItems[i];
            double totalCost = item.cost * item.amount;
            if (totalCost <= remainingBudget) {
                for (int j = 0; j <= k; j++) {
                    if (items[j] == item) {
                        items[j].status = "Куплено";
                        break;
                    }
                }
                remainingBudget -= totalCost;
                boughtCount++;
                out.println("Куплен: " + item.name + " за " + String.format("%.2f", totalCost));
            } else {
                out.println("Не удалось купить: " + item.name + " (не хватает " +
                        String.format("%.2f", totalCost - remainingBudget) + ")");
            }
        }
        out.println("Куплено товаров: " + boughtCount + " из " + count);
        out.println("Остаток бюджета: " + String.format("%.2f", remainingBudget));
        return remainingBudget;
    }
}
```
