package SauceDemo;


import java.io.File;
import java.io.FileInputStream;
import java.io.IOException;
import org.apache.poi.xssf.usermodel.XSSFSheet;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;
import org.openqa.selenium.By;
import org.openqa.selenium.JavascriptExecutor;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.Select;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;


public class SauceDemo_Test

{
	
	 private WebDriver driver;
	 
//Browser Installation
	
	@BeforeTest
	public void Browser() throws InterruptedException, IOException
    {
		
		
		try {
			
		
			System.setProperty("webdriver.chrome.driver","D:\\abdul\\selenium\\Selenium_Software\\Chromedriver2021\\chromedriver.exe");
			 driver = new ChromeDriver();
			 driver.manage().window().maximize();
		        	
         driver.get("demosaucedemo.com/"); 
          Thread.sleep(2000);
    
		}
		
		catch(Exception ex)
		{
			
			System.out.println(ex.getMessage()); 
			return;
		}
	     
					}
	
   //login with username & Password with excel
  
	@Test(priority=1)
	public void Saucelogin() throws InterruptedException, IOException

	{
        XSSFSheet sh1;
        
 File src=new File("D:\\abdul\\selenium\\Trustrace-login\\TrusTracelogin details.xlsx");
 FileInputStream fis=new FileInputStream(src);
 XSSFWorkbook w =new XSSFWorkbook(fis);

  sh1= w.getSheetAt(0);


driver.get("https://www.saucedemo.com/");
System.out.println("Title:"+ driver.getTitle());
try
{
        
int row=1; 
{

String username = sh1.getRow(row).getCell(0).getStringCellValue();
System.out.println("Username "+username);


driver.findElement(By.id("user-name")).sendKeys(username);
String password = sh1.getRow(row).getCell(1).getStringCellValue();

System.out.println("Password "+password);
driver.findElement(By.id("password")).sendKeys(password);
Thread.sleep(3000);

driver.findElement(By.id("login-button")).click();

}
}

catch (Exception e) 
{

System.out.println(e.getMessage());

}
	}
	
	
	@Test(priority=2)
	public void Sorting() throws InterruptedException, IOException

	{
try
{
	
	// Sort by Low to high
	WebElement Low = driver.findElement(By.xpath("//*[@id=\"inventory_filter_container\"]/select"));
	Low.click();
	driver.findElement(By.xpath("//*[@id=\"inventory_filter_container\"]/select/option[4]")).click();
	Thread.sleep(6000);
	
	//Sort by Z to A

	driver.findElement(By.xpath("//*[@id=\"inventory_filter_container\"]/select")).click();
	driver.findElement(By.xpath("//*[@id=\"inventory_filter_container\"]/select/option[2]")).click();
	Thread.sleep(6000);
	
	
	// Sort by A/Z
	driver.findElement(By.xpath("//*[@id=\"inventory_filter_container\"]/select")).click();
	driver.findElement(By.xpath("//*[@id=\"inventory_filter_container\"]/select/option[1]")).click();
	Thread.sleep(6000);
	
	// Sort by high to low
	driver.findElement(By.xpath("//*[@id=\"inventory_filter_container\"]/select")).click();
	driver.findElement(By.xpath("//*[@id=\"inventory_filter_container\"]/select/option[4]")).click();
	Thread.sleep(6000);
}

catch (Exception e) 
{

System.out.println(e.getMessage());

}
	}
	

	@Test(priority=3)
	public void AddProduct() throws InterruptedException, IOException

	{
try
{
	    
	//Scroll downn and add Product
	 JavascriptExecutor js = (JavascriptExecutor) driver;
	 js.executeScript("window.scrollBy(0,1000)");
	 driver.findElement(By.xpath("//*[@id=\"item_3_title_link\"]/div")).click();
	 
	 //Add to cart button
	 driver.findElement(By.xpath("//*[@id=\"inventory_item_container\"]/div/div/div/button")).click();
	
	//Shopping cart icon
	 driver.findElement(By.cssSelector(" #shopping_cart_container > a > svg")).click();
	 Thread.sleep(5000);
	 
	//Get product name to fine duplicate in cart page or not
	 
	String result1= driver.findElement(By.id("item_3_title_link")).getText();
	String string = result1;
	String[] parts = string.split("(  )");
	String part1 = parts[0]; 
	System.out.println(part1); 
	

    if (part1.equals("Test.allTheThings() T-Shirt (Red)"))

	  {
    	
    	driver.findElement(By.xpath("//*[@id=\"cart_contents_container\"]/div/div[2]/a[2]")).click();
    	
		}
    
    else
	  {

          driver.findElement(By.xpath("//*[@id=\"cart_contents_container\"]/div/div[1]/div[3]/div[2]/div[2]/button")).click();

	  }
	  	
}

catch (Exception e) 
{

System.out.println(e.getMessage());

}
	}
	
	@Test(priority=4)
	public void Checkout() throws InterruptedException, IOException
{
		try
		{
			
    //Filling Name & Address
		   
		WebElement Firstname = driver.findElement(By.id("first-name"));
		Firstname.sendKeys("abdul");
		
		WebElement Lastname = driver.findElement(By.id("last-name"));
		Lastname.sendKeys("Rahman");
		
		WebElement Postcode = driver.findElement(By.id("postal-code"));
		Postcode.sendKeys("641002");
		Thread.sleep(3000);
		
		
		//Click checkout button
		driver.findElement(By.xpath("//*[@id=\"checkout_info_container\"]/div/form/div[2]/input")).click();
		
		JavascriptExecutor js = (JavascriptExecutor) driver;
		 js.executeScript("window.scrollBy(0,1000)");
		 
		 //Clcik finish button
		 driver.findElement(By.xpath("//*[@id=\"checkout_summary_container\"]/div/div[2]/div[8]/a[2]")).click();
			
	}
      
catch (Exception e) 
{

System.out.println(e.getMessage());

}
	}
	
	
	
	@AfterTest
	public void BrowserQuit() throws InterruptedException, IOException
    {
	
	driver.quit();
    }
}

