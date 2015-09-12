package com.ebay;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.ie.InternetExplorerDriver;
import org.testng.annotations.AfterClass;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.Parameters;
import org.testng.annotations.Test;

public class MultiBrowser {

	public WebDriver driver;

	@Parameters("browser")
	@BeforeClass
	// Passing Browser parameter from TestNG xml
	public void lunchbrowser(String browser) throws Exception {

		// If the browser is Firefox, then do this

		if (browser.equalsIgnoreCase("firefox")) {

			driver = new FirefoxDriver();

			// If browser is IE, then do this

		} else if (browser.equalsIgnoreCase("ie")) {

			// Here I am setting up the path for my IEDriver

			System.setProperty(
					"webdriver.ie.driver",
					"C:\\Users\\sumaia\\Desktop\\Jars_file\\IEDriverServer_x64_2.46.0\\IEDriverServer.exe");
Thread.sleep(1000);
			driver = new InternetExplorerDriver();

		}

		// Doesn't the browser type, lauch the Website

		driver.get("https://www.google.com/");

	}

	// Once Before method is completed, Test method will start
	@Test(priority = 2)
	public void google(){
driver.findElement(By.xpath(".//*[@id='lst-ib']")).sendKeys("Enam is a good boy");
System.out.println("Searchinh google");
driver.quit();
	}
	@Test(priority = 1)
	public void signin() throws Exception {
		System.out.println("I am doing ebay signin ");
		WebDriver driver = new FirefoxDriver();
		driver.get("http://www.ebay.com/");
		driver.findElement(By.xpath(".//*[@id='gh-ug']/a")).click();

		Thread.sleep(1000);

		driver.findElement(By.id("userid")).sendKeys("enammd");
		driver.findElement(By.id("pass")).sendKeys("ehaque9839");

		Thread.sleep(1000);

		// driver.findElement(By.id("signed_in")).clear();
		driver.findElement(By.id("sgnBt")).click();

		driver.findElement(By.id("gh-ac")).sendKeys("sd card for foscam");
		driver.findElement(By.id("gh-btn")).click();
		driver.quit();
	}

	@Test(priority = 0)
	public void signout() throws Exception {
		System.out.println("I am doing ebay sign out");
		WebDriver driver = new FirefoxDriver();
		driver.get("http://www.ebay.com/");
		driver.findElement(By.xpath(".//*[@id='gh-ug']/a")).click();

		Thread.sleep(1000);

		driver.findElement(By.id("userid")).sendKeys("enammd");
		driver.findElement(By.id("pass")).sendKeys("ehaque9839");

		Thread.sleep(1000);

		// driver.findElement(By.id("signed_in")).clear();
		driver.findElement(By.id("sgnBt")).click();

		
		driver.quit();
	}

	@AfterClass
	public void closebrowser() {

		driver.quit();

	}

}