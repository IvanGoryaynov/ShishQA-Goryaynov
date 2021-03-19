import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.support.ui.Select;
import org.testng.Assert;
import org.testng.annotations.AfterClass;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.Test;

import java.util.concurrent.TimeUnit;

import static org.testng.Assert.assertEquals;

public class First {
    private WebDriver driver;
    private String baseUrl;
    @BeforeClass(alwaysRun = true)
    public void setUp() throws Exception {
        System.setProperty("webdriver.chrome.driver", "src/test/chromedriver.exe");
        driver = new ChromeDriver();
        baseUrl = "https://sandbox.cardpay.com/MI/cardpayment2.html?orderXml=PE9SREVSIFdBTExFVF9JRD0nODI5OScgT1JERVJfTlVNQkVSPSc0NTgyMTEnIEFNT1VOVD0nMjkxLjg2JyBDVVJSRU5DWT0nRVVSJyAgRU1BSUw9J2N1c3RvbWVyQGV4YW1wbGUuY29tJz4KPEFERFJFU1MgQ09VTlRSWT0nVVNBJyBTVEFURT0nTlknIFpJUD0nMTAwMDEnIENJVFk9J05ZJyBTVFJFRVQ9JzY3NyBTVFJFRVQnIFBIT05FPSc4NzY5OTA5MCcgVFlQRT0nQklMTElORycvPgo8L09SREVSPg==&sha512=998150a2b27484b776a1628bfe7505a9cb430f276dfa35b14315c1c8f03381a90490f6608f0dcff789273e05926cd782e1bb941418a9673f43c47595aa7b8b0d";
        driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
    }
    @Test
    public void testFirstTestCase() throws Exception {
        driver.get(baseUrl);
        // ERROR: Caught exception [ERROR: Unsupported command [typeKeys | id=input-card-number | 4000 0000 0000 0036]]
        driver.findElement(By.id("input-card-number")).sendKeys("4000000000000036");
        driver.findElement(By.id("input-card-holder")).clear();
        driver.findElement(By.id("input-card-holder")).sendKeys("IVAN GORYAYNOV");
        new Select(driver.findElement(By.id("card-expires-month"))).selectByVisibleText("07");
        new Select(driver.findElement(By.id("card-expires-year"))).selectByVisibleText("2037");
        driver.findElement(By.id("input-card-cvc")).clear();
        driver.findElement(By.id("input-card-cvc")).sendKeys("007");
        driver.findElement(By.id("action-submit")).click();
        assertEquals(driver.findElement(By.xpath("//div[@id='payment-item-cardholder']/div[2]")).getText(), "IVAN GORYAYNOV");
        driver.findElement(By.xpath("//div[@id='payment-item-total']/div[2]")).click();
        Assert.assertEquals(driver.findElement(By.id("payment-item-total-amount")).getText(), "291.86");
        driver.findElement(By.xpath("//div[@id='payment-item-status']/div[2]")).click();
        driver.findElement(By.xpath("//div[@id='payment-item-status']/div[2]")).click();
        // ERROR: Caught exception [ERROR: Unsupported command [doubleClick | //div[@id='payment-item-status']/div[2] | ]]
        assertEquals(driver.findElement(By.xpath("//div[@id='payment-item-status']/div[2]")).getText(), "Confirmed");

    }


    @Test
    public void testSecondTestCase() throws Exception {
        Actions actions = new Actions(driver);
        driver.get(baseUrl);
        // ERROR: Caught exception [ERROR: Unsupported command [typeKeys | id=input-card-number | 4000 0000 0000 0036]]
        driver.findElement(By.id("input-card-number")).sendKeys("4000000000000036");
        driver.findElement(By.id("input-card-holder")).clear();
        driver.findElement(By.id("input-card-holder")).sendKeys("IVAN GORYAYNOV");
        new Select(driver.findElement(By.id("card-expires-month"))).selectByVisibleText("10");
        new Select(driver.findElement(By.id("card-expires-year"))).selectByVisibleText("2022");
        driver.findElement(By.id("input-card-cvc")).clear();
        driver.findElement(By.id("input-card-cvc")).sendKeys("077");
        driver.findElement(By.id("action-submit")).click();
        assertEquals(driver.findElement(By.xpath("//div[@id='payment-item-cardholder']/div[2]")).getText(), "IVAN GORYAYNOV");
        driver.findElement(By.xpath("//div[@id='payment-item-total']/div[2]")).click();
        Assert.assertEquals(driver.findElement(By.id("payment-item-total-amount")).getText(), "291.86");
        driver.findElement(By.xpath("//div[@id='payment-item-status']/div[2]")).click();
        driver.findElement(By.xpath("//div[@id='payment-item-status']/div[2]")).click();
        // ERROR: Caught exception [ERROR: Unsupported command [doubleClick | //div[@id='payment-item-status']/div[2] | ]]
        assertEquals(driver.findElement(By.xpath("//div[@id='payment-item-status']/div[2]")).getText(), "Confirmed");
    }
    @Test
    public void testThirdTestCase() throws Exception {
        driver.get(baseUrl);
        // ERROR: Caught exception [ERROR: Unsupported command [typeKeys | id=input-card-number | 4000 0000 0000 0036]]
        driver.findElement(By.id("input-card-number")).sendKeys("5555555555554444");
        driver.findElement(By.id("input-card-holder")).clear();
        driver.findElement(By.id("input-card-holder")).sendKeys("IVAN GORYAYNOV");
        new Select(driver.findElement(By.id("card-expires-month"))).selectByVisibleText("09");
        new Select(driver.findElement(By.id("card-expires-year"))).selectByVisibleText("2025");
        driver.findElement(By.id("input-card-cvc")).clear();
        driver.findElement(By.id("input-card-cvc")).sendKeys("257");
        driver.findElement(By.id("action-submit")).click();
        driver.findElement(By.id("success")).submit();
        assertEquals(driver.findElement(By.xpath("//div[@id='payment-item-cardholder']/div[2]")).getText(), "IVAN GORYAYNOV");
        driver.findElement(By.xpath("//div[@id='payment-item-total']/div[2]")).click();
        assertEquals(driver.findElement(By.id("payment-item-total-amount")).getText(), "291.86");
        driver.findElement(By.xpath("//div[@id='payment-item-status']/div[2]")).click();
        driver.findElement(By.xpath("//div[@id='payment-item-status']/div[2]")).click();
        // ERROR: Caught exception [ERROR: Unsupported command [doubleClick | //div[@id='payment-item-status']/div[2] | ]]
        assertEquals(driver.findElement(By.xpath("//div[@id='payment-item-status']/div[2]")).getText(), "Declined by issuing bank");
    }


    @AfterClass(alwaysRun = true)
    public void tearDown() throws Exception {
        driver.quit();
    }
}