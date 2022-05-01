unity脚本 日记
ctrl+shirf+C= console
向上移动
 transform.Translate(Vector3.up*Time.deltatime*3)


转向
public  void Move()
{
    float h=Input.GetAxis ("Horizontal");
    if(Mathf.Abs(h)>0.1f)
   {
      if(h>0)
       transform.LocalRotation=Quaternion.Euler(0,0,0);
      elsewoz
       transform.LocalRotation=Quaternion.Euler(0,180,0);
       transform.Translate(h*Vector3.right*Time.deltaTime);
       ani.Setbool{"Run",true};
   }
     else
     ani.Setbool{"Run",false};
}


飞机大站中的  飞机跟随鼠标
void OnMouseDrag()
{
Vector3 targetPos=Camera.main.ScreenToWorldPoint(Input.mousePosition);         鼠标坐标是一个
targetPos.z=1;                                          二维坐标，所以固定 z，z不能大于相机到背景 的距离
targetPos.x=Mathf.Clamp(targetPos.x,-2.3f,2.3f);
targetPos.y=Mathf.Clamp(targetPos.z,-4.5f,4.5f);
transform.position=targetPos;
}

飞机大战中的  背景滚动（利用Renerer中的SetTextureOffset）
public lcass PlayerControl:MonoBehaviour
{
  private GameObject bg;
 }
void Start()
{
  bg=GameObject.Find("BG");
}
void Update()
{
bg.Getcomponent<Renderer>().material.SetTextureOffset("_MainTex"，new Vector2(0,Time.time/5))
}
//每五秒钟一次背景



子弹生成
bulletPrefab=Resources.Load<GameObject>("Bullet");
 ...
private   void Attack()
{
 GameObject=Instantiate(bulletPrefab,firePos.position,firePos.rotation);
}



InvokeRepeating("attack",0,0.5f)     0表示刚开始运行时调用一次，0.5表示每0.5秒调用一


控制移动的代码
void Update （）
{
float moveX=Input.GetAxisRaw("Horizontal");//控制水平移动方向 A表示-1 D表示1 不按为0
float moveY=Input.GetAxisRaw("Vettical");//控制垂直移动方向    W表示1    S表示-1 不按为0

Vector2  position=transform.position;
 position.x+=moveX*speed*Time.deltaTime;
 position.y+=moveY*speed*Time.deltaTIme;
transform.positino=position;
}

导航  (记得添加组件NavMeshAgent,t为目标位置)
using UnityEngine.AI
public class EnemyAI:MonoBehaviour
{
    private NavMeshAgent agent;
    public Transform t;
      void Start()
   {
      agent=GetComponent<NavMeshAgent>();
      agent.destination=t.position;
    }
}


有东西碰到加命的草莓时(PlayerController是玩家的脚本)
void   OnTriggerEnter2D(Collider2D other)
{
PlayerController  pc=other.GetComponent<PlayerController> ();
  if(pc!=null)
  { 
    Debug.log("玩家碰到了草莓") ；
   }
}
  
 在B类中设置属性  方便A类访问
private int maxHealth=5;//最大生命值
private   int currentHealth;//当前生命值
public int MyMaxHealth{get{return maxHealth;}}
punlic int MyCurrentHealth{get{return currentHealth;}}



Ruby Adventure
持续在陷阱会受到伤害
void OnTriggerStay2D (Collider2D other)
{
 PlayerController pc=other.GetComponent<PlayerController>();
 if(pc!=null)
   {
      pc.ChangeHealth(-1);
    }
}     
 
费血的方法
private void ChangeHealth(int amount)
{
  if(amout<0)
   {
       if(isInvincible==true) 
         {return;}
        isInvincible=true;
        invincibleTimer=invincibleTime;
    }
  Debug.Log(currentHealth+"/"+maxHealth);
currentHealth=Mathf.Clamp(currentHealth+amount,0,maxHealth);
 Debug.Log(currentHealth+"/"+maxHealth);
}


敌人移动（是否垂直，进行来回的水平和上下移动）
public float speed=3;
public bool isVertical;
public float changeDirectionTime= 2f;
private Vector2 moveDirection;
private RigidBody2D rbody;
private float changeTimer;
void Start()
{
rbody=GetComponent<RigidBody2D>();
moveDirection=isVertical?Vector2.up:Vector2.right;
changeTimer=changeDIrectionTime;
}
void Update()
{
changeTimer-=Time.deltaTime;
if(changeTImer<0)
{
moveDIrection*=-1;
changeTimer=changeDirectionTime;
}
Vector2 position=rbody.position;
position.x+=moveDirection.x*speed*Time.deltaTime;
position.y+=moveDirection.y*speed*Time.deltaTime;
rbody.MovePosition(position);
}


人物的对话框  
player-canvas-image-text     canvas这里记得调成world space    字不清晰可以给text添加outline

       

对话框的消失与隐藏
public GameObject dialogImage;//对话
public float showTime=4;
private float showTimer;
void Start()
{
dialogImage.SetActive(false);//初始默认隐藏对话框
showTimer=-1;
}
void Update()
{
   showTimer-=Time.deltaTime;
   if(showTimer<0)
    {
       dialogTimie.Setactive(false);
     }
}
public void ShowDialog()
{
  showTimer=showTime;
dialogImage.SetActive(True);
}



过滤模式 选择  点








背景循环
public float speed=5f;
void Start ()
{}
void   Update()
{
 Vector2 v=transform.localPosition;
 v.y-=speed*Time.deltaTime;             //7.6是地图的长    4是4个地图
     if(v.y>7.6f)
         {
           v.y-=4*7.6f;
          }
 transform.localPosition=v;
}



AudioSource.PlayClipPoint(clips,firePos.position,0.5f)
片段 位置 大小
UnityEditor.EditorApplication.isPlayingll


！！！！！把刚体中的sleeping mode  由start awake 改成 never sleep  可以持续进行检测，站在陷阱里不动会一直费血
！！！！把  Sprite Renderer里的  Draw Mode  由 simple改成Tiled 这时候 拉物体不会变形



用单例播放声音  
public class AudioManager:MonoBehaviour{

private static  AudioManager instance{get;private set;}
public AudioSource audioS;
void  Start()
 {
   instance=this;
   audioS=GetComponent<AudioSource>();
  }
public   void AudioPlay(AudioClip clip)
 {
       audios.PlayOneShot(clip);
 }
   

public Audioclip fixedClip


AudioManager.instance.AudioPlay(fixedClip)


Quaternion.Slerp
这个方法的意思其实就是：让初始点面朝目标点。第三个参数的意思是让初始点转多少度才能面朝目标点。参数意思是从from 的rotation慢慢旋转增值到to.rotation.以多少的角度旋转，把其中的值插到这个中间过程中，就是这个方法所要表达的意思。



敌人的AI
思路：  检查前面是否有障碍物让敌人朝向玩家，往前走，
             左右两边两条射线碰撞检测，如果碰到障碍物，敌人就开始旋转，
              后边左右发出两条射线，如果喷到障碍物，则意味敌人面前没障碍物
public class EnemyAI:MonoBehaviour{
  private int range;
  private float speed;
  private bool isThereAnything=false;

  public GameObject target;
  private float rotationSpeed;
  private RaycastHit hit;
 void Start()
{
   range=80;
   speed=10f;
   rotationSpeed=15f;
}

void Update()
{
      //检查前面是否障碍物
     if(!isThereAnyThing)
      {
          Vector3 relativePos=target.transform.position-transform.position;
          Quaterninon rotation=Quaternion.LookRotation(relaivePos);
          transform.rotation=Quaternion.Slerp(transform.rotation,rotation,Time.deltaTime*speed);
      }
    transform.Translate(Vector3.forward*Time.deltaTime*speed);
   
   Transform leftRay=transform;
   Transform rightRay=transform;

     //左右两个射线检测碰撞，碰到障碍物就旋转
     if(Physics.Raycast(leftRay.position+(transform.right*7)，transform.forward,out hit ,range)||
     Physics.Raycast(rightRay.position-(transform.right*7),transform.forard,out hit ,range))
        {
            if(hit.collider.tag=="Obstacles")
             {
                   isThereAnything=true;
                  transform.Rotation(Vector3.up*Time.deltaTime*RotationSpeed);
             }
        }
     //后面两边两个射线检测碰撞，碰碍物就意味着玩家面前没障碍物
      if(Physics.Raycast(transform.position-(transform.forward*4),transform.right,out hit ,10)||
        Physics.Raycast(transfom.position-(transform.forward*4),-transofrm.right,out hit 10) 
         {
               if(hit.collider.gameObject.CompareTag("Obstacles"))
                  {  isThereAnything=false;}
         }        
}





敌人AI（蝙蝠飞向敌人）

MoveTowards(float current, float target, float maxDelta);
current The current value.当前值
target The value to move towards.要移向的值
maxDelta The maximum change that should be applied to the value.应用到该值的最大变化
public class EemySmartBat :Enemy{
   public float speed;
   public float  radius;//检测半径

  public Transform playerTransform; 
    void Start()
     {
          base.Start();
         playerTransform=GameObject.FindGameObjectWithTag("player").GetComponent<Transform>                           ();
     }
    void Update()
     {
        base.Update();
        if(playerTransform!=null)
         {
             float distance=(transform.posiition-playerTransform.positon).sqrMagnitude;
              if(distance<radius)
                {
                      transform.position=Vector2.MoveTowards(transform.positon,
                                                                                          playerTransform.position,
                                                                                          speed*Time.deltaTime);
                }
         } 
    }
}
小蛇左右爬行AI
public class EnemySnake:Enemy
{
  public float speed;
  public float waitTime;
  public Transform[] movePos;
 
  private int i=0;
  private bool movingRight=true;
  private float wait;
   
  void Start()
   {
     base.Start();
      wait=waitTime;
   }
   void Update()
   {
      base.Update();
     transform.position=
    Vector2.MoveTowards(transform.positon,move[i].position,speed*Time.deltaTime);
     if(Vecto2.Distance(transform.positoin,movePos[i].positoin)<0.1f)
      {
            if(waitTime>0)
          {
                       waitTime-=Time.deltaTime;
          }
          else
           {
              if(movingRight)
               {
                         transform.eulerAngles=new Vector3(0,-180,0);
                         movingRight=false;
               }
               else 
               {
                    transform.eulerAngles= new Vector3(0,0,0);
                    movingRight=true;
               }
               if(i==0)
                   {
                      i=1;
                   }
               else  
                   {
                      i=0;
                    }
               waitTime=wait;
           }
      }
   }
}



背包系统的5个脚本 （点击能使用，也可以点×放回去,第五个是效果  其他slot的效果可以改，等同于5个）

 public class Inventory:MonoBehaviour
{
    public bool[]  isFull;
    public GameObject[] slots;
}


public class PickUp:MonoBehaviour
{
      private Inventory inventory;
      public GameObject itemButton;

     private void Start()
     {
         inventory=GameObject.FindGameObjectWithTag("Player").GetComponent<Inventory>();
     }
    private void Update()
     {
           if(other.CompareTag("Player")&&other.GetType().ToString()=="UnityEngine.BoxCollider2D")
           {
               for(int i=0;i<inventory.slots.Length;i++)
                 {
                           if(inventory.slots[i]==false)
                           {
                                       inventory.slots[i]==true;
                                       Instantiate(itemButton,inventory.slots[i].transform,false);
                                       Destroy(gameObject);
                                       break;
                           }
                  }
           }
     }
}

public class slot:MonoBehaviour
{
         private Inventory inventory;
         public int i;
         private void Start()
          {
                                inventory=GameObject.FindGameObjectWithTag("Player").GetComponent<Inventory>();
          }
         private void Update()
         {
                  if(transform.childCount<=0)
                   {
                         inventory.isFull[i]==false;
                    }
         }
       public void DropItem()
        {
            foreach(Transform child in transform)
             {
                    child.GetComponent<Spawn>().SpawnDroppedItem();
                    GameObject.Destroy(child.gameObject);
             }
        }
}



public class Spawn:MonoBehaviour
{
     public GameObject item;
     private Transform player;
     private void   Start()
     {
               player=GameObject.FindGameObjectWithTag("Player").transform;
     }
     public void SpawnDroppedItem()
     {
              Vector2 playerPos=new Vector2(player.position.x+1,player.position.y);
               Instantiate(item,playerPos,Quaternion.identity);
     }
}


public class CoinEffect:MonoBehaviour()
{
  public GameObject effect;
  private Transform player;
  private void Start()
  {
        player=GameObject.FindGameObjectWithTag("Player").transform;
  }
  public void Use()
  {
          Instantiate(effect,player.position,Quaternion.identity);
           Destroy(gameObject);
  }

}



多次跳跃



public class PlayerController:MonoBehaviour
{
     private Rigidbody2D rb;
     public float  speed;
     public float jumpForce;
     private float moveInput;
      
     private bool isGround;  
     public Transform featPos;
     public float checkRadius;
     public LayerMask whatIsGround;


     private float jumpTimeCounter;
     public float jumpTime;
     private bool isJumping;
      void Start()
       {
               rb=GetComponent<Rigidbody2D>();
       }
      void FixedUpdate()
       {
             moveInput=Input.GetAxisRaw("Horizontal");
            rb.velocity=new Vector2(moveInput*speed,rb.velocity.y);
       }
       void Update()
       {
            isGround=Physics2D.OverlapCircle(featPos.position,checkRaduis,whatIsGround);
             if(moveInput>0)
              {
                   transform.eulerAngles=new Vector3(0,0,0);
              }
             if(moveInput<=0)
              {
                transform.eulerAngles=new Vector3(0,180,0);
              }
            if(isGround==true&&Input.GetKeyDown(KeyCode.Space))
             {
                    isJumping=true;
                     jumpTimeCounter=jumpTime;
                    rb.velocity=Vector2.up*jumpForce;
             }
            if(Input.GetKey(KeyCode.Space&&isJumping==true))
             {
                 if(jumpCounter>0)
                  {
                      rb.velocity=Vector2.up*jumpForce;
                      jumpCounter-=Time.deltaTime;
                  }
                 else
                  {
                         isJumping=false;
                   }
             }
             if(Input.GetKeyUp(KeyCode.Space))
              {
                  isJumping=false;
              }
       }
     
}







EventSystems.IsPointerOverGameObject   判断是否为UI元素
！IsPointerOverGameObject   是要当前为UI元素

要与UI元素交互，必须要勾上Blocks Raycast
不与UI元素交互，要关掉BlocksRaycast ，不然操作会冲突




这代码意思是 当前右键按下  且 按下的是非ui元素



List.Find(x=>x.MyBagScript.isOpened())//List.Find() 查找是否有符合的元素，只要有一个符合，则返回true

 背包系统总开关      
public void openClose()
{
    //如果有关着的（则意味着一定有开着的，也有没开的），isClosed为true；如果没有关着的，意味着都开了，isClosed为false
    bool isClosed = bagList.Find(x => !x.MyBagScript.isOpened);//List.Find 表示是否存在一个符合条件的元素
  
    
    //如果有关着的，那么要让没有关着的打开；如果没有关着的，那么就全都打开
    foreach (Bag bag in bagList)
    {
        if (bag.MyBagScript.isOpened != isClosed)
        {
           bag.MyBagScript.OpenClose();
        }
    }
}





