---
title: 工厂模式
date: 2015-01-07 12:18:54
tags:
- 设计模式
categories:
- 杂
---


<p><span style="font-size:16px; color:#000099"><strong><span class="link_title"><a href="http://blog.csdn.net/hguisu/article/details/7505909">转自 ：设计模式一 工厂模式Factory</a></span></strong></span></p>
<p><span style="font-size:16px; color:#000099"><strong></strong></span></p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;在面向对象编程中, 最通常的方法是一个new操作符产生一个对象实例,new操作符就是用来构造对象实例的。但是在一些情况下, new操作符直接生成对象会带来一些问题。举例来说, 许多类型对象的创造需要一系列的步骤: 你可能需要计算或取得对象的初始设置; 选择生成哪个子对象实例; 或在生成你需要的对象之前必须先生成一些辅助功能的对象。 在这些情况,新对象的建立就是一个 “过程”，不仅是一个操作，像一部大机器中的一个齿轮传动。</p>
<p></p>
<p><strong>模式的问题</strong>：你如何能轻松方便地构造对象实例，而不必关心构造对象实例的细节和复杂过程呢？</p>
<strong>解决方案</strong>：<a href="http://blog.csdn.net/hguisu/article/details/7505909">建立一个工厂来创建对象</a>。
<p><strong>实现：</strong></p>
<p><span style="font-size:16px">
<h1 id=引言>引言</h1>
</span>&nbsp; &nbsp; <span style="font-family:Arial">1）还没有工厂时代：假如还没有工业革命，如果一个客户要一款宝马车,一般的做法是客户去创建一款宝马车，然后拿来用。<br>
&nbsp;&nbsp;&nbsp; 2）简单工厂模式：后来出现工业革命。用户不用去创建宝马车。因为客户有一个工厂来帮他创建宝马.想要什么车，这个工厂就可以建。比如想要320i系列车。工厂就创建这个系列的车。即工厂可以创建产品。<br>
&nbsp; &nbsp; 3）工厂方法模式时代：为了满足客户，宝马车系列越来越多，如320i，523i,30li等系列一个工厂无法创建所有的宝马系列。于是由单独分出来多个具体的工厂。每个具体工厂创建一种系列。即具体工厂类只能创建一个具体产品。但是宝马工厂还是个抽象。你需要指定某个具体的工厂才能生产车出来。<br>
&nbsp;&nbsp;&nbsp; 4）抽象工厂模式时代：随着客户的要求越来越高，宝马车必须配置空调。而且这空调必须对应给系列车才能使用。于是这个工厂开始生产宝马车和需要的空调。<br>
&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 最终是客户只要对宝马的销售员说：我要523i空调车，销售员就直接给他523i空调车了。而不用自己去创建523i空调车宝马车.<br>
&nbsp; &nbsp;（我只是举个例子，说到宝马配置空调完全是为了举例，甚至有点扯，哪有车和空调必须对应才能使用啊）<br>
&nbsp; &nbsp; &nbsp;这就是工厂模式。<br>
<span style="font-size:16px">
<h1 id="分类">分类</h1></span>&nbsp;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;工厂模式主要是为创建对象提供过渡接口，以便将创建对象的具体过程屏蔽隔离起来，达到提高灵活性的目的。&nbsp;<br>
工厂模式可以分为三类：&nbsp;<br>
1）<a href="http://blog.csdn.net/hguisu/article/details/7505909">简单工厂模式</a>（Simple Factory）&nbsp;<br>
2）<a href="http://blog.csdn.net/hguisu/article/details/7505909">工厂方法模式</a>（Factory Method）&nbsp;<br>
3）<a href="http://blog.csdn.net/hguisu/article/details/7505909">抽象工厂模式</a>（Abstract Factory）&nbsp;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 这三种模式从上到下逐步抽象，并且更具一般性。&nbsp;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GOF在《设计模式》一书中将工厂模式分为两类：工厂方法模式（Factory Method）与抽象工厂模式（Abstract Factory）。将简单工厂模式（Simple Factory）看为工厂方法模式的一种特例，两者归为一类。&nbsp;<br>
<span style="font-size:16px">
<h1 id="区别">区别</h1>
</span>工厂方法模式：<br>
一个抽象产品类，可以派生出多个具体产品类。 &nbsp;&nbsp;<br>
一个抽象工厂类，可以派生出多个具体工厂类。 &nbsp;&nbsp;<br>
每个具体工厂类只能创建一个具体产品类的实例。<br>
抽象工厂模式：<br>
多个抽象产品类，每个抽象产品类可以派生出多个具体产品类。 &nbsp;&nbsp;<br>
一个抽象工厂类，可以派生出多个具体工厂类。 &nbsp;&nbsp;<br>
每个具体工厂类可以创建多个具体产品类的实例。 &nbsp;&nbsp;<br>
区别：<br>
工厂方法模式只有一个抽象产品类，而抽象工厂模式有多个。 &nbsp;&nbsp;<br>
工厂方法模式的具体工厂类只能创建一个具体产品类的实例，而抽象工厂模式可以创建多个。</span><br>
两者皆可。&nbsp;</p>
<p><br>
<span style="font-size:16px">
<h1 id="简单工厂模式">简单工厂模式</h1>
</span>建立一个工厂（一个函数或一个类方法）来制造新的对象。<br>
分布说明引子：从无到有。客户自己创建宝马车，然后拿来用。<br>
&nbsp;<img alt="" src="http://my.csdn.net/uploads/201204/25/1335357036_2095.jpg"><br>
<br>
<br>
</p>
<pre class="php" name="code">&lt;?php
/**
 * 车子系列
 *
 */
Class BWM320{
function __construct($pa) {

}
}
Class BMW523{
   function __construc($pb){

}
}

/**
 * 
 * 客户自己创建宝马车
 */
class Customer {

   function createBMW320(){
       return new BWM320();
   }

   function createBMW523(){
       return new BMW523();
   }
} </pre>
<p><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <strong><span style="color:#ff6600">客户需要知道怎么去创建一款车,客户和车就紧密耦合在一起了.为了降低耦合</span></strong>,就出现了工厂类,把创建宝马的操作细节都放到了工厂里面去,客户直接使用工厂的创建工厂方法,传入想要的宝马车型号就行了,而不必去知道创建的细节.这就是工业革命了：<strong>简单工厂模式</strong></p>
<p>即我们建立一个工厂类方法来制造新的对象。如图：</p>
<p><img src="http://my.csdn.net/uploads/201204/26/1335407364_5745.jpg" alt=""><br>
</p>
<p><br>
产品类：</p>
<pre class="php" name="code">&lt;?php
/**
 * 车子系列
 *
 */
abstract Class BWM{
    function __construct($pa) {

    }
}
Class BWM320 extends BWM{
    function __construct($pa) {

    }
}
Class BMW523 extends BWM{
   function __construc($pb){

   }
}


</pre>
<p>&nbsp;工厂类：</p>
<pre class="php" name="code">/**
 * 
 * 工厂创建车
 */
class Factory {


    static function  createBMW($type){
        switch ($type) {
          case 320:
             return new BWM320();
          case 523:
             return new BMW523();
        //....
   }
}
</pre>
<p>客户类：</p>
<pre class="php" name="code">/**
 * 
 * 客户通过工厂获取车
 */
class Customer {
    private $BMW;
    function getBMW($type){
        $this¬-&gt; BMW =  Factory::createBMW($type);
    }
}

</pre>
<p><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 简单工厂模式又称静态工厂方法模式。从命名上就可以看出这个模式一定很简单。它存在的目的很简单：定义一个用于创建对象的接口。&nbsp;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;先来看看它的组成：&nbsp;<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;1) 工厂类角色：这是本模式的核心，含有一定的商业逻辑和判断逻辑。<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;2) 抽象产品角色：它一般是具体产品继承的父类或者实现的接口。 &nbsp; &nbsp; &nbsp; &nbsp;&nbsp;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 3) 具体产品角色：工厂类所创建的对象就是此角色的实例。在java中由一个具体类实现。&nbsp;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;下面我们从开闭原则（对扩展开放；对修改封闭）上来分析下简单工厂模式。当客户不再满足现有的车型号的时候，想要一种速度快的新型车，只要这种车符合抽象产品制定的合同，那么只要通知工厂类知道就可以被客户使用了。所以对产品部分来说，它是符合开闭原则的；但是工厂部分好像不太理想，<strong><span style="color:#ff6600">因为每增加一种新型车，都要在工厂类中增加相应的创建业务逻辑（createBMW($type)方法需要新增case），这显然是违背开闭原则的</span></strong>。可想而知对于新产品的加入，工厂类是很被动的。对于这样的工厂类，我们称它为全能类
 或者上帝类。&nbsp;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;我们举的例子是最简单的情况，而在实际应用中，很可能产品是一个多层次的树状结构。由于简单工厂模式中只有一个工厂类来对应这些产品，所以这可能会把我们的上帝累坏了，也累坏了我们这些程序员:(&nbsp;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;于是工厂方法模式作为救世主出现了。 工厂类定义成了接口,而每新增的车种类型,就增加该车种类型对应工厂类的实现,这样工厂的设计就可以扩展了,而不必去修改原来的代码。<br>
<h1 id="工厂方法模式">工厂方法模式</h1>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;工厂方法模式去掉了简单工厂模式中工厂方法的静态属性，使得它可以被子类继承。这样在简单工厂模式里集中在工厂方法上的压力可以由工厂方法模式里不同的工厂子类来分担。&nbsp;<br>
工厂方法模式组成：&nbsp;<br>
&nbsp; &nbsp; &nbsp; &nbsp;1)抽象工厂角色： 这是工厂方法模式的核心，它与应用程序无关。是具体工厂角色必须实现的接口或者必须继承的父类。在java中它由抽象类或者接口来实现。&nbsp;<br>
&nbsp; &nbsp; &nbsp; &nbsp;2)具体工厂角色：它含有和具体业务逻辑有关的代码。由应用程序调用以创建对应的具体产品的对象。&nbsp;<br>
&nbsp; &nbsp; &nbsp; &nbsp;3)抽象产品角色：它是具体产品继承的父类或者是实现的接口。在java中一般有抽象类或者接口来实现。&nbsp;<br>
&nbsp; &nbsp; &nbsp; &nbsp;4)具体产品角色：具体工厂角色所创建的对象就是此角色的实例。在java中由具体的类来实现。&nbsp;<br>
&nbsp; &nbsp; &nbsp; &nbsp;工厂方法模式使用继承自抽象工厂角色的多个子类来代替简单工厂模式中的“上帝类”。正如上面所说，这样便分担了对象承受的压力；而且这样使得结构变得灵活 起来——当有新的产品产生时，只要按照抽象产品角色、抽象工厂角色提供的合同来生成，那么就可以被客户使用，而不必去修改任何已有 的代码。可以看出工厂角色的结构也是符合开闭原则的！&nbsp;<br>
&nbsp;</p>
<p><img src="http://my.csdn.net/uploads/201204/26/1335434907_6359.jpg" alt=""><br>
代码如下：&nbsp;</p>
<p>产品类：</p>
<pre class="php" name="code">&lt;?php
/**
 * 车子系列
 *
 */
abstract Class BWM{
function __construct($pa) {

}
}
Class BWM320 extends BWM{
function __construct($pa) {

}
}
Class BMW523 extends BWM{
   function __construc($pb){

}
}

</pre>
<p><br>
创建工厂类：</p>
<pre class="php" name="code">/**
 * 创建工厂的接口
 *
 */
interface FactoryBMW { 
       function createBMW(); 
} 


/**
 * 
 * 创建BWM320车
 */
class FactoryBWM320 implements FactoryBMW {
   function  createBMW($type){
      return new BWM320();
   }

}


/**
 * 
 * 创建BWM523车
 */
class FactoryBWM523 implements FactoryBMW {
   function  createBMW($type){
      return new BMW523();
   }
}

</pre>
<p><br>
客户类：</p>
<pre class="php" name="code">/**
 * 
 * 客户得到车
 */
class Customer {
   private $BMW;
   function  getBMW($type){
      switch ($type) {
        case 320:
           $BWM320 = new FactoryBWM320();
           return $BWM320-&gt;createBMW();
        case 523:
           $BWM523 = new FactoryBWM523();
           return $BWM320-&gt;createBMW();
            //....
      }

  }
}

</pre>
<p><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 可以看出工厂方法的加入，使得对象的数量成倍增长。当产品种类非常多时，会出现大量的与之对应的工厂对象，这不是我们所希望的。因为如果不能避免这种情 况，可以考虑使用简单工厂模式与工厂方法模式相结合的方式来减少工厂类：即对于产品树上类&#20284;的种类（一般是树的叶子中互为兄弟的）使用简单工厂模式来实 现。<br>
<strong></strong></p>
<p><strong>工厂方法小结： <br>
</strong>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 工厂方法模式仿佛已经很完美的对对象的创建进行了包装，使得客户程序中仅仅处理抽象产品角色提供的接口。那我们是否一定要在代码中遍布工厂呢？大可不必。也许在下面<span style="color:#ff0000">情况下你可以考虑使用工厂方法模式：&nbsp;<br>
&nbsp;&nbsp;&nbsp;&nbsp; 1)当客户程序不需要知道要使用对象的创建过程。&nbsp;<br>
&nbsp;&nbsp;&nbsp;&nbsp; 2)客户程序使用的对象存在变动的可能，或者根本就不知道使用哪一个具体的对象。 </span></p>
<span style="color:#ff0000"></span>
<p><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 简单工厂模式与工厂方法模式真正的避免了代码的改动了？没有。在简单工厂模式中，新产品的加入要修改工厂角色中的判断语句；而在工厂方法模式中，要么将判 断逻辑留在抽象工厂角色中，要么在客户程序中将具体工厂角色写死（就象上面的例子一样）。而且产品对象创建条件的改变必然会引起工厂角色的修改。<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 面对这种情况，我们可以使用反射机制：</p>
<pre class="php" name="code"> class Customer {
     private $BMW;
     function  getBMW($type){
         $class = new ReflectionClass('FactoryBWM' .$type );//建立 'FactoryBWM'这个类的反射类  
          $instance  = $class-&gt;newInstanceArgs();//相当于实例化'FactoryBWM' .$type类  
          return $instance-&gt;createBMW();
        //或者直接 
         /**
         * $instance = new 'FactoryBWM' .$type();
         * return $instance-&gt;createBMW();
         */
    }
}
</pre>
<p><span style="font-size:16px"><strong></strong></span>&nbsp;</p>
<p><span style="font-size:16px">
<h1 id="抽象工厂模式">抽象工厂模式</h1>
</span><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 随着客户的要求越来越高，宝马车需要配置空调。于是这个工厂开始生产宝马车和配置需要的空调。这时候工厂有二个系列的产品:宝马车和空调.宝马车必须使用对应的空调才能使用.这时候分别使用一个车工厂和一个空调工厂都不能满足我们的需求,我们必须确认车跟空调的对应关系。因此把车工厂跟空调工厂联系在一起。因此出现了抽象工厂模式。<br>
&nbsp;&nbsp;&nbsp;&nbsp; 可以说，抽象工厂模式和工厂方法模式的区别就在于需要创建对象的复杂程度上。而且抽象工厂模式是三个里面最为抽象、最具一般性的。 <br>
抽象工厂模式的用意为：给客户端提供一个接口，可以创建多个产品族中的产品对象 ，<span style="color:#ff0000">而且使用抽象工厂模式还要满足一下条件：<br>
&nbsp;&nbsp;&nbsp;&nbsp; 1)系统中有多个产品族，而系统一次只可能消费其中一族产品。 <br>
&nbsp;&nbsp;&nbsp;&nbsp; 2)同属于同一个产品族的产品以其使用。 <br>
</span>抽象工厂模式的各个角色（和工厂方法一样）： <br>
&nbsp;&nbsp;&nbsp;&nbsp; 1)抽象工厂角色： 这是工厂方法模式的核心，它与应用程序无关。是具体工厂角色必须实现的接口或者必须继承的父类。在java中它由抽象类或者接口来实现。&nbsp;<br>
&nbsp;&nbsp;&nbsp;&nbsp; 2)具体工厂角色：它含有和具体业务逻辑有关的代码。由应用程序调用以创建对应的具体产品的对象。<br>
&nbsp;&nbsp;&nbsp;&nbsp; 3)抽象产品角色：它是具体产品继承的父类或者是实现的接口。<br>
&nbsp;&nbsp;&nbsp;&nbsp; 4)具体产品角色：具体工厂角色所创建的对象就是此角色的实例。</p>
<p>&nbsp;</p>
<p>其结构：</p>
<p><img alt="" src="http://my.csdn.net/uploads/201204/25/1335357105_2682.jpg"><br>
</p>
<p>&nbsp;<br>
我们的例子：<br>
&nbsp;<img src="http://my.csdn.net/uploads/201204/26/1335434941_2951.jpg" alt=""><br>
<br>
代码：</p>
<p>产品类：<br>
</p>
<pre class="php" name="code">&lt;?php
/**
 * 车子系列以及型号
 *
 */
abstract class  BWM{
}

class BWM523 extends  BWM {
}
class BWM320 extends  BWM {


}
/**
 * 空调
 *
 */
abstract class aircondition{
}
class airconditionBWM320  extends aircondition {

}
class airconditionBWM52 extends aircondition {

}

</pre>创建工厂类：<br>
<br>
<pre class="php" name="code">/**
 * 创建工厂的接口
 *
 */
interface FactoryBMW { 
     function createBMW(); 
     function createAirC(); 
} 


/**
 * 
 * 创建BWM320车
 */
class FactoryBWM320 implements FactoryBMW {
    function  createBMW(){
    return new BWM320();
}
function  createAirC(){ //空调
    return new airconditionBWM320();
}
}


/**
 * 
 * 创建BWM523车
 */
class FactoryBWM523 implements FactoryBMW {
    function  createBMW(){
    return new BWM523();
}
function  createAirC(){
    return new airconditionBWM523();
}
}

</pre>客户:<br>
<p></p>
<pre class="php" name="code">/**
 * 
 * 客户得到车
 */
class Customer {
   private $BMW;
   private $airC;
   function  getBMW($type){
       $class = new ReflectionClass('FactoryBWM' .$type );//建立 Person这个类的反射类  
        $instance  = $class-&gt;newInstanceArgs();//相当于实例化Person 类  
        $this-&gt;BMW =  $instance-&gt;createBMW();
       $this-&gt;airC =  $instance-&gt;createAirC();
   }
}

</pre>
<p><br>
</p>
   
</div>