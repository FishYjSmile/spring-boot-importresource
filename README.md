## Sprintboot （一）@Importresource、@ConfigurationProperties
以前的bean是通过xml文件导入，若还想通过xml可以使用@Importresource

@ImportResource("classpath:文件名.xml")  //导入spring的配置文件
@ConfigurationProperties     配置绑定

eg:mysql账户密码等等

 

controller中的文件配置

复制代码
public class springcontrol {

    @Autowired     //自动注入 ，因为在pojo类中已经将Car设置了加入容器
    Car car;
}
@RequestMapping("/Car")
public Car car() {
    return car;
}
复制代码
application.properties配置信息

mycar.brand = BYD
mycar.price = 10000
POJO类配置信息

复制代码
package spring.main.spring.Bean;


import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.stereotype.Component;

/*
只有在容器中的组件才会有springboot提供的功能
 */
@Component   //将组件加入到容器中
@ConfigurationProperties(prefix = "mycar")    //配置绑定，绑定application.properties
public class Car {
    private String brand;
    private Integer price;

    public String getBrand() {
        return brand;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }

    public Integer getPrice() {
        return price;
    }

    public void setPrice(Integer price) {
        this.price = price;
    }

    public Car(String brand, Integer price) {
        this.brand = brand;
        this.price = price;
    }

    public Car() {
    }

    @Override
    public String toString() {
        return "Car{" +
                "brand='" + brand + '\'' +
                ", price=" + price +
                '}';
    }
}
复制代码
@Component   //将组件加入到容器中
@ConfigurationProperties(prefix = "mycar")    //配置绑定，绑定application.properties
/*
只有在容器中的组件才会有springboot提供的功能
 */

之后发现在application.properties里的信息进行了一一绑定
