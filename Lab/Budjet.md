``` java
class Budjet {
    public double sum;
    @Override
    public String toString() {
        return String.format("%.2f",sum);
    }
    public Budjet(double sum) {
        if (sum < 0) {
            this.sum = 0;
        }
        else {
            this.sum = sum;
        }
    }
    public void setSum(double a) {
        if (sum < 0) {
            this.sum = 0;
        }
        else {
            this.sum = a;
        }
    }
    public void plussum(double a) {
        this.sum = sum + a;
    }
}
```
