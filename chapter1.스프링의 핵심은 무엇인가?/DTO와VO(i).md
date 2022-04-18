# DTO 와 VO
데이터를 위한 객체를 만들다보면 DTO와 VO의 언급이 잦은데, 이 둘이 헤깔리는 경우가 많다. 
그래서 이번에 확실히 정리해보고자 한다. 

## DTO(Data Transfer Object)
- 순수하게 데이터를 담아 계층간으로 전달하는 객체이다. 
- 로직을 갖고 있지 않은 순수한 데이터 객체이다. 
- 메소드로는 getter/setter만을 갖는다. 
  - setter로 값을 담아내고, getter를 이용하여 값을 꺼내 쓴다.
 ```
 public class CarDTO {
	private String modelName; // 모델명
	private int size; // 크기
	private int fuelefficiency;// 연비
	private int output; // 출력
	private int price; // 가격

	public String getModelName() {
		return modelName;
	}

	public void setModelName(String modelName) {
		this.modelName = modelName;
	}

	public int getSize() {
		return size;
	}

	public void setSize(int size) {
		this.size = size;
	}

	public int getFuelefficiency() {
		return fuelefficiency;
	}

	public void setFuelefficiency(int fuelefficiency) {
		this.fuelefficiency = fuelefficiency;
	}

	public int getOutput() {
		return output;
	}

	public void setOutput(int output) {
		this.output = output;
	}

	public int getPrice() {
		return price;
	}

	public void setPrice(int price) {
		this.price = price;
	}

}

 ```
## VO(Value Object)
- 값 그 자체를 나타내는 객체
- DTO와 반대로 로직을 포함하고 있다.
- VO의 경우 특정 값 자체를 표현하기 때문에 불변성의 보장을 위해 생성자를 사용하여야 한다.
 ```
public class CarVO {
	private String name;
	private int modelID;
	private int option;
	
	public CarVO(String name,int modelID, int option ) {
		this.name = name;
		this.modelID = modelID;
		this.option = option;
	}
	
	
	public void camera() {
		
	}
	public void navigation() {
		
	}
	
	public void autoSensor() {
	}
}

 ```
 
 ### 비교 
 크게 비교하자면 DTO는 값의 전달이 목적이고, VO는 값을 표현하는게 목적이다. 
 
 ||DTO|VO|
 |--|--|--|
 |목적|계층간 데이터 전달|값 자체 표현|
 |동등성|필드값이 같아도 같은 객체가 아님|필드값이 같으면 같은 객체|
 |가변성|가변적임|불변적임|
 |로직|getter/setter외의 로직이 필요하지않음|생성자가 있으며, getter/setter외 로직이 있음|
 
 
- 하지만, 굳이 이둘을 나누어 쓰기보다는 혼용해서 쓰는 경우도 있다보니, 이게 맞다! 저게 맞다! 라고 하기에는 어려운것 같다.
