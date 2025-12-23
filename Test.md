``` java
public class popo {
    public static Scanner in = new Scanner(System.in);
    public static PrintStream out = System.out;

    public static void main(String[] args) throws IOException {
                out.println("Создаем новый список и бюджет:");
                Budjet b1 = new Budjet(800.0);
                Spisok s1 = new Spisok();

                out.println("Начальный бюджет: " + b1);
                out.println("Увеличиваем бюджет:");
                b1.plussum(200.0);
                out.println("Измененный бюджет: " + b1);
                s1.add("Хлеб", 50.0, 2, "Не куплено");
                s1.add("Молоко", 80.0, 1, "Не куплено");
                s1.add("Мясо", 300.0, 1, "Не куплено");
                s1.add("Сыр", 200.0, 1, "Не куплено");
                s1.add("Яблоки", 120.0, 2, "Не куплено");
                out.println("" + s1);
                out.println("Могу ли я купить товар №1?");
                s1.dostatochno1(1, b1.sum);
                out.println();
                out.println("Могу ли я купить товар №3?");
                s1.dostatochno1(3, b1.sum);
                out.println();
                out.println("Могу ли я купить всё?");
                s1.kupluvse(b1.sum);
                out.println();
                out.println("Сколько мне не хватает для покупки всего списка?");
                s1.nehvataet(b1.sum);
                out.println();
                out.println("Попытка купить товар №1");
                b1.sum = s1.pokupka(1, b1.sum);
                out.println("Текущий бюджет: " + b1);
                out.println("" + s1);
                out.println("Полная стоимость списка: " + s1.polnayacost());
                out.println("Стоимость некупленных товаров: " + s1.fullnekupleno());
                out.println("Сортируем список по убыванию и возрастанию цены:");
                s1.sorte();
                out.println("" + s1);
                s1.sortp();
                out.println("" + s1);
                out.println("Самый дорогой товар:");
                s1.samydor();
                out.println("Самый дешевый товар:");
                out.println(s1.samydesh());
                out.println();
                out.println("Создаем новый список и бюджет:");
                Budjet b2 = new Budjet(1000.0);
                Spisok s2 = new Spisok();

                out.println("Начальный бюджет: " + b2);
                s2.add("Хлеб", 50.0, 2, "Не куплено");
                s2.add("Молоко", 80.0, 1, "Не куплено");
                s2.add("Мясо", 300.0, 1, "Не куплено");
                s2.add("Сыр", 200.0, 1, "Не куплено");
                s2.add("Яблоки", 120.0, 2, "Не куплено");

                out.println("" + s2);
                out.println("Попытка купить все товары, начиная с самых дешевых:");
                out.println("Начальный бюджет: " + b2);
                b2.sum = s2.kupitVse(b2.sum, true);
                out.println("" + s2);
                out.println();
                out.println("Создаем новый список и бюджет:");
                Budjet b3 = new Budjet(600.0);
                Spisok s3 = new Spisok();

                out.println("Начальный бюджет: " + b3);

                // Добавляем товары
                s3.add("Хлеб", 50.0, 2, "Не куплено");
                s3.add("Молоко", 80.0, 1, "Не куплено");
                s3.add("Мясо", 300.0, 1, "Не куплено");
                s3.add("Сыр", 200.0, 1, "Не куплено");
                s3.add("Яблоки", 120.0, 2, "Не куплено");

                out.println("" + s3);
                out.println("Попытка купить все товары, начиная с самых дешевых, а затем с самых дорогих при недостатке бюджета:");
                out.println("Начальный бюджет: " + b3);
                b3.sum = s3.kupitVse(b3.sum, true);
                out.println("" + s3);

                out.println("Бюджет: " + b3);
                b3.sum = s3.kupitVse(b3.sum, false);
                out.println("" + s3);
                out.println();
                out.println("Создаем новый список и бюджет:");

                Budjet b4 = new Budjet(1000.0);
                Spisok s4 = new Spisok();

                out.println("Начальный бюджет: " + b4);

                // Добавляем товары
                s4.add("Хлеб", 50.0, 2, "Не куплено");
                s4.add("Молоко", 80.0, 1, "Не куплено");
                s4.add("Мясо", 300.0, 1, "Не куплено");
                s4.add("Сыр", 200.0, 1, "Не куплено");
                s4.add("Яблоки", 120.0, 2, "Не куплено");

                out.println("" + s4);
                out.println("Попытка купить 3 товара, начиная с дешевых");
                b4.sum = s4.kupitKolvo(b4.sum, 3, true);
                out.println("" + s4);
    }
}
```
