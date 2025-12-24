``` java
class Budjet {
    public double sum;
    @Override
    // Вывод бюджета в строковом формате
    public String toString() {
        return String.format("%.2f",sum);
    }
    // Создание нового бюджета
    public Budjet(double sum) {
        if (sum < 0) {
            this.sum = 0;
        }
        else {
            this.sum = sum;
        }
    }
    // Создание неуказанного бюджета
    public Budjet() {
        this.sum = 0;
    }
    // Изменение бюджета
    public void setSum(double a) {
        if (sum < 0) {
            this.sum = 0;
        }
        else {
            this.sum = a;
        }
    }
    // Увеличение бюджета
    public void plussum(double a) {
        if (sum + a < 0) {
            this.sum = 0;
        }
        else {
            this.sum = sum + a;
        }
    }
}
```
