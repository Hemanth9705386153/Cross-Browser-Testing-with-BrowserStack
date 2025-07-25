# Cross-Browser-Testing-with-BrowserStack
TEST 4

package browserstack;

import java.net.URL;
import java.util.HashMap;

import org.openqa.selenium.By;
import org.openqa.selenium.MutableCapabilities;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.remote.RemoteWebDriver;

public class CrossBrowserTest {

    public static final String USERNAME = "hemanthvanka_rXCzwG"; 
    public static final String AUTOMATE_KEY = "VUGdEE5su2WAzWrBWKU5";
    public static final String BROWSERSTACK_URL = "https://" + USERNAME + ":" + AUTOMATE_KEY + "@hub-cloud.browserstack.com/wd/hub";

    public static void main(String[] args) throws Exception {
        WebDriver driver = null;

        try {
      //       ✅ W3C-compliant capabilities
            MutableCapabilities capabilities = new MutableCapabilities();
            capabilities.setCapability("browserName", "Chrome");
            capabilities.setCapability("browserName", "Firefox");
            capabilities.setCapability("browserName", "Edge");


            capabilities.setCapability("browserVersion", "latest");

            HashMap<String, Object> bstackOptions = new HashMap<String, Object>();
            bstackOptions.put("os", "Windows");
            bstackOptions.put("osVersion", "10");
            bstackOptions.put("projectName", "SauceDemo CrossBrowser Test");
            bstackOptions.put("buildName", "Build 1.0");
            bstackOptions.put("sessionName", "CrossBrowserTest");

            // Attach BrowserStack options
            capabilities.setCapability("bstack:options", bstackOptions);

            driver = new RemoteWebDriver(new URL(BROWSERSTACK_URL), capabilities);

            driver.get("https://www.saucedemo.com/");

            // Perform login
            driver.findElement(By.id("user-name")).sendKeys("standard_user");
            driver.findElement(By.id("password")).sendKeys("secret_sauce");
            driver.findElement(By.id("login-button")).click();

            String currentURL = driver.getCurrentUrl();
            if (currentURL.contains("inventory")) {
                System.out.println("✅ Login successful!");
            } else {
                System.out.println("❌ Login failed.");
            }

        } catch (Exception e) {
            System.out.println("❌ Test failed due to: " + e.getMessage());
        } finally {
            if (driver != null) {
                driver.quit();
            }
        }
    }
}
