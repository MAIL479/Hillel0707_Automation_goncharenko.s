package HomeWork27;

import io.github.bonigarcia.wdm.WebDriverManager;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.WebDriverWait;
import org.testng.Assert;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.BeforeMethod;
import org.testng.annotations.Test;

import java.time.Duration;
import java.util.List;

public class Homework27 {

    private WebDriver driver;
    private WebDriverWait wait;
    final String URL = "https://rozetka.com.ua/ua/";

    @BeforeMethod
    public void before() {
        WebDriverManager.chromedriver().setup();
        driver = new ChromeDriver();
        wait = new WebDriverWait(driver, Duration.ofSeconds(10));
        driver.manage().window().maximize();
        driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
        driver.get(URL);
    }

    @Test
    public void rozetkaTest() {
        List<WebElement> saleGoods = driver.findElements(By.xpath("(//ul[contains(@class, 'main-goods')])[1]/li"));
        int countOfGoods = saleGoods.size();
        Assert.assertEquals(countOfGoods, 6, "The number of promotional items is not equal to 6");

        WebElement itemPrice = driver.findElement(By.xpath("(//ul[contains(@class, 'main-goods')])[1]/li[1]//div[contains(@class, 'price_color_red')]"));
        String itemPriceValue = itemPrice.getAttribute("innerText").replaceAll(" ", "");

        WebElement firstProduct = driver.findElement(By.xpath("(//ul[contains(@class, 'main-goods')])[1]/li[1]"));
        firstProduct.click();

        WebElement priceOnProductPage = driver.findElement(By.xpath("//p[contains(@class, 'prices__big')]"));
        String priceOnProductPageValue = priceOnProductPage.getAttribute("innerText").trim();

        Assert.assertEquals(itemPriceValue, priceOnProductPageValue, "Prices on the main and product pages do not match");

        driver.navigate().back();

        String currentURL = driver.getCurrentUrl();
        Assert.assertEquals(currentURL, URL, "URL do not match");

        List<WebElement> saleGoodsNew = driver.findElements(By.xpath("(//ul[contains(@class, 'main-goods')])[4]/li"));
        int countOfGoodsNew = saleGoodsNew.size();
        Assert.assertEquals(countOfGoodsNew, 6, "The number of promotional items is not equal to 6 after returning to the main page");
    }

    @AfterMethod
    public void after() {
        driver.quit();
    }
}
