package TestMaven.PrasadTreeni;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;
import java.util.concurrent.TimeUnit;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;

import io.github.bonigarcia.wdm.WebDriverManager;

public class Assign1 {

	public static void main(String[] args) throws Exception
	{
		WebDriverManager.chromedriver().setup();
		WebDriver driver=new ChromeDriver();
		driver.manage().window().maximize();   //Maximize the windows
		driver.manage().timeouts().implicitlyWait(10,TimeUnit.SECONDS);    //implicutly wait
		driver.get("https://stackoverflow.com");   // Open the stackoverflow site is open
		Thread.sleep(1000);
		driver.findElement(By.xpath("//button[@id='onetrust-accept-btn-handler']")).click();   // popup accepted
		Thread.sleep(3000);
		driver.findElement(By.xpath("//a[@class='s-topbar--menu-btn js-left-sidebar-toggle']")).click();    //“Browse Questions click
		Thread.sleep(1000);
		driver.findElement(By.xpath("//a[@id='nav-users']")).click();    //Click on users.
		Thread.sleep(1000);
		driver.findElement(By.xpath("//a[contains(text(),'Editors')]")).click();    // The user click on Editor option.

		Thread.sleep(2000);
		driver.findElement(By.xpath("//a[contains(text(),'Next')]")).click();  //Click on Second page ((pagination)
		Thread.sleep(1000);

	    List<WebElement> webE = driver.findElements(By.xpath("//div[@class='-flair']"));
		
		int  sizeOfvalue =webE.size();
		System.out.println("Total value in:- " +sizeOfvalue);  // Total number of Element present in page.

		ArrayList<Integer> array=new ArrayList<Integer>();    // create the new arraylist
		for(int i=0;i<sizeOfvalue;i++)
		{
		 WebElement value = webE.get(i);
		 int aV = Integer.parseInt(value.getText());                        // Converted into Integer format 
		 array.add(aV);                                                                     // Add the value in array list one by one.
		}

		int number = HighNumber(array);                                        //Calling the Highest value method.
		
		System.out.println(" The max value is " + number);
		
		List<WebElement> web2 = driver.findElements(By.xpath("//div[@class='-flair']"));
		for(int i=0;i<web2.size();i++)
		{
		 WebElement value2 = web2.get(i);
		 int aV1 = Integer.parseInt(value2.getText());
		 if(number==aV1)
		 {
			         List<WebElement> userName = value2.findElements(By.xpath("//div[@class='-flair']/parent::div/a"));
			         WebElement uValue = userName.get(i);
			        System.out.println("The user name is:- "+ uValue.getText());
			        Thread.sleep(1000);
		             List<WebElement> location = value2.findElements(By.xpath("//span[@class='user-location']"));
		             WebElement lValue = location.get(i);
		             System.out.println( "The location is :- " + lValue.getText());
		             Thread.sleep(1000);
		             List<WebElement> Edits = value2.findElements(By.xpath("//div[@class='user-tags']"));
		             WebElement eValue = Edits.get(i);
		            System.out.println("The edits are:- " + eValue.getText());
		    }
		}
	
	  	driver.close();        //Close the browser 

		}


		public static int HighNumber(ArrayList<Integer> array)
		{
		int maximum=0;
		        for (int i = 1; i < array.size(); i++)
		        {
		            if (maximum < array.get(i))
		                maximum = array.get(i);
		        }
		        return maximum;

		 }
	}



