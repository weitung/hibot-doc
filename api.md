# HIBOT_API
#參數設定
目前將各模組的連接以及參數定義於`handler_setting.xml`中

### 模組間的連接
現在利用`handler_setting.xml`中的`<slave><No>`定義連接的順序，外接的模組主要分為兩大體系：Festo, Akribis，這兩個體系內的各模組彼此之間是串聯的。因此下列的資料便可定義一個slave：

	<slave>
			<No type="festo">3</No>
			<HibotID type="single">festo.2</HibotID>
			<Device>CMMT-AS</Device>
	</slave>
	
其中`<No>`的`type`屬性定義了這個slave是屬於哪一個體系，而值則代表此為串聯的第3個模組，將直接透過網路線連接到電腦的定義為第1個模組。  
  
`<HibotID>`的值是在使用api宣告的時候所要使用的參數，在使用時必須宣告有定義的ID。其中`type`屬性為`single`代表ID就完全等於`<HibotID>`的值；如果為`multiple`則代表宣告時所用的ID還需要參考子項目的`<HibotID>`的值定義，兩者之間用`.`連接。  

`<Device>`的值代表這個模組的型號

### 硬體參數
最根本的模組會需要一些參數的定義，定義在需要定義的模組的`<Params>`中，範例如下：

	<Params>
			<param>
				<Index>6098</Index>
				<SubIndex>0</SubIndex>
				<Description>Default Homing Method</Description>
				<Value>17</Value>
			</param>
	<Params>

在`<Params>`中可能有許多`<param>`，而`<param>`中的`<Value>`為設定的值。

## API使用
要使用HIBOT_API，需引入`hibot_server.h`
### 馬達
	class Motor{
	public:
	    explicit Motor(std::string id);
	    std::string id;
	    
	    // Controls (Synchronous)
	    int motor_home(int vel, int acc, int offset, int mode);
	    int motor_ptp(int tgtpos, int vel, int acc, int deacc);
	    
	    // Monitors (Synchronous)
	    std::string motor_monitor();
	}
	
在宣告Motor時，需輸入其對應的id，以連結到對應的馬達控制。  

`motor_home `是用來控制馬達回零的函式，有四項參數`int vel, int acc, int offset, int mode`，其中`vel`為回零速度；`acc`為回零加速度；`offset`為回零後往反方向的偏移量；`mode`為回零模式，回零模式的數字意義請參考參數說明。  

`motor_ptp `是用來控制馬達到指定點的函式，有四項參數`int tgtpos, int vel, int acc, int deacc`，其中`tgtpos`為目標的絕對位置，單位為電機的step；`vel`為移動速度；`acc`為達到移動速度的加速度；`deacc`為即將抵達目標前的減速度。  

`motor_monitor`會回傳一個字串，其中包含此馬達個各個狀態，日後會提供確定的格式以及相對應的解碼函式。
### IO Module
	class IO{
	public:
	    explicit IO(std::string id);
	    std::string id;
	    
	    // Controls (Synchronous)
	    int io_set(int tgtval, int pinout);
	    
	    // Monitors (Synchronous)
	    std::string io_monitor();
	}
	
在宣告IO Module時，需輸入其對應的id，以連結到對應的IO控制。   

`io_set`為控制IO Output的函式，有兩項參數`int tgtval, int opmode`，其中`tgtval`為輸出的目標值，通常只有0或1；`pinout`為想要輸出的孔位。  

`io_monitor `會回傳一個字串，其中包含將此Module的Input Status，日後會提供確定的格式以及相對應的解碼函式。

