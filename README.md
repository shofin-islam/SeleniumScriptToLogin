# SeleniumScriptToLogin
selenium script to login https://www.blessingurls.com/nsitpm ,change the user name and check it works or not.


package FirstSeleniumTest;

import java.util.List;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.firefox.FirefoxDriver;

public class FirstInterractionTest {
	static WebDriver driver;
    static WebElement select;
    static WebElement xyz;
   
    public static void main(String[] args) {
        String projectLocation = System.getProperty("user.dir");
        System.out.println(projectLocation);
        System.setProperty("webdriver.gecko.driver", "E:\\Automation\\SeleniumProject\\lib\\geckodriver\\geckodriver.exe");
        driver = new FirefoxDriver();
        login();        
        System.out.println(driver.getCurrentUrl());
        if (driver.getCurrentUrl().contains("https://www.blessingurls.com/nsitpm/admin_master.php")) {
            System.out.println("Login Successfully");
            changeUserName("Change Name");
            logOut("Logout");
            login();
            logOut("Logout");
            driver.quit();
        }
    }

    public static void changeUserName(String optionName) {
            driver.findElement(By.className("dropdown-toggle")).click();
            select = driver.findElement(By.xpath("//ul[@class='dropdown-menu dropdown-user']")); // Find the drop down
            List<WebElement> options = select.findElements(By.tagName("li"));
            for (WebElement opt : options) {
                if (opt.getText().equals(optionName)) {
                    opt.click();
                    driver.findElement(By.name("change_name")).sendKeys("Shofin");
                    driver.findElement(By.name("btn")).click();
                    return;
                }
            }
    }
   
    public static void logOut(String logout) {
        driver.findElement(By.className("dropdown-toggle")).click();
        xyz = driver.findElement(By.xpath("//ul"));
        List<WebElement> options = xyz.findElements(By.tagName("li"));
        for (WebElement opt : options) {
            if (opt.getText().equals(logout)) {
                opt.click();
                return;
            }
        }
    }
   
    public static void login() {
        driver.get("https://www.blessingurls.com/nsitpm/");
        driver.findElement(By.name("email_address")).sendKeys("safiul.islam@edison-bd.com");
        driver.findElement(By.name("password")).sendKeys("123456");
        driver.findElement(By.name("btn")).click();
        return;
    }
}
