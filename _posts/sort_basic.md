<h2><span style="font-family: 幼圆;">写在前面：</span></h2>
<p>&nbsp;1.图片来源是从别的博客转来的，后期有空会自己使用java swing实现。</p>
<p>&nbsp;2.代码实现由于个人习惯使用了C++和python，<a href="https://zhuanlan.zhihu.com/p/57088609">https://zhuanlan.zhihu.com/p/57088609</a>博主实现了java版本。</p>
<p>&nbsp;3.这里的代码实现排序顺序都是从左到右的升序。想要实现逆序可以直接颠倒数组。其实所谓的&ldquo;小&rdquo;只是相对的，&ldquo;小&rdquo;的规则可以通过重载运算符或者传入比较器，比较函数来实现自己想要的标准，来变成&ldquo;大&rdquo;</p>
<h2><span style="font-family: 幼圆;">1.冒泡排序（bubble sort）</span></h2>
<h3>1.1 算法过程：</h3>
<p>　　比方对于一个从左到右排列的数组。比较相邻的元素。如果左边比第右边大，就交换他们两个。对每一对相邻元素作同样的工作，从开始第一对到尾部的最后一对。这样尾部的元素将会是最大的元素。从左到右（除尾端的）每个元素依次作为起点重复上述的步骤。&nbsp;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp;算法名字很形象，每一个元素就是慢慢浮动到自己应该在的位置。借《啊哈！算法》中的一个图来理解</p>
<p><img style="width: 300px; height: 300px; margin-left: 10%;" src="https://img2020.cnblogs.com/i-beta/1958859/202003/1958859-20200304150426277-1242741343.png" alt="" /></p>
<h3>1.2 可视化展示：</h3>
<p><img style="margin-left: 5%;" src="https://img2020.cnblogs.com/blog/1958859/202003/1958859-20200304181426541-582293997.gif" alt="" /></p>
<p>图源：<a href="https://juejin.im/post/5b4d8c47e51d4519105d4ec3">https://juejin.im/post/5b4d8c47e51d4519105d4ec3</a></p>
<h3>1.3 代码：</h3>
<p>python版本：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">def</span><span style="color: #000000;"> bubble_sort(nums):
    length </span>=<span style="color: #000000;"> len(nums)
    </span><span style="color: #0000ff;">if</span>(length==<span style="color: #000000;">0):
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> nums
    </span><span style="color: #0000ff;">for</span> i <span style="color: #0000ff;">in</span><span style="color: #000000;"> range(length):
        </span><span style="color: #0000ff;">for</span> j <span style="color: #0000ff;">in</span><span style="color: #000000;"> range(i,length):
            </span><span style="color: #0000ff;">if</span> nums[i]&gt;<span style="color: #000000;">nums[j]:
                nums[i],nums[j] </span>=<span style="color: #000000;"> nums[j],nums[i]
    </span><span style="color: #0000ff;">return</span> nums</pre>
</div>
<p>C++版本：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> template&lt;typename T&gt; 
<span style="color: #008080;">2</span> <span style="color: #0000ff;">void</span> bubbleSort(T arr[], <span style="color: #0000ff;">int</span><span style="color: #000000;"> length) {
</span><span style="color: #008080;">3</span>     <span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; length - <span style="color: #800080;">1</span>; i++<span style="color: #000000;">){
</span><span style="color: #008080;">4</span>         <span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> j = <span style="color: #800080;">0</span>; j &lt; length- <span style="color: #800080;">1</span> - i; j++<span style="color: #000000;">)
</span><span style="color: #008080;">5</span>             <span style="color: #0000ff;">if</span> (arr[j] &gt; arr[j + <span style="color: #800080;">1</span><span style="color: #000000;">])
</span><span style="color: #008080;">6</span>                 swap(arr[j], arr[j + <span style="color: #800080;">1</span><span style="color: #000000;">]);
</span><span style="color: #008080;">7</span> <span style="color: #000000;">    }
</span><span style="color: #008080;">8</span> }  </pre>
</div>
<p>&nbsp;</p>
<h3>1.4 算法改进</h3>
<p>　　优化1：设立一个&ldquo;flag&rdquo;，记录每一次遍历过程中是否发生了交换。若没有发生交换说明数组已经是有序的了，可以提前退出循环。</p>
<p>　　优化2：可以记录最后一次发生交换的位置，此位置之后的元素已经是有序的，不需要再进行遍历。</p>
<p>　　实现优化1（C++）：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;"> 1</span> template&lt;typename T&gt;
<span style="color: #008080;"> 2</span> <span style="color: #0000ff;">void</span> bubbleSort( T arr[] , <span style="color: #0000ff;">int</span><span style="color: #000000;"> length){
</span><span style="color: #008080;"> 3</span> 
<span style="color: #008080;"> 4</span>     <span style="color: #0000ff;">bool</span><span style="color: #000000;"> swapped;
</span><span style="color: #008080;"> 5</span> 
<span style="color: #008080;"> 6</span>     <span style="color: #0000ff;">do</span><span style="color: #000000;">{
</span><span style="color: #008080;"> 7</span>         swapped = <span style="color: #0000ff;">false</span><span style="color: #000000;">;
</span><span style="color: #008080;"> 8</span>         <span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span>; i &lt; length - <span style="color: #800080;">1</span>; i++<span style="color: #000000;">)
</span><span style="color: #008080;"> 9</span>             <span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> j = <span style="color: #800080;">0</span>; j &lt; length - <span style="color: #800080;">1</span> - i; j++<span style="color: #000000;">)
</span><span style="color: #008080;">10</span>                 <span style="color: #0000ff;">if</span> (arr[j] &gt; arr[j + <span style="color: #800080;">1</span><span style="color: #000000;">]){
</span><span style="color: #008080;">11</span>                     swap(arr[j], arr[j + <span style="color: #800080;">1</span><span style="color: #000000;">]);
</span><span style="color: #008080;">12</span>                     swapped=<span style="color: #0000ff;">true</span><span style="color: #000000;">;
</span><span style="color: #008080;">13</span> <span style="color: #000000;">        }
</span><span style="color: #008080;">14</span> 
<span style="color: #008080;">15</span>     }<span style="color: #0000ff;">while</span><span style="color: #000000;">(swapped);
</span><span style="color: #008080;">16</span> }</pre>
</div>
<p>　　实现优化2(C++)：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;"> 1</span> template&lt;typename T&gt;
<span style="color: #008080;"> 2</span> <span style="color: #0000ff;">void</span> bubbleSort( T arr[] , <span style="color: #0000ff;">int</span><span style="color: #000000;"> n){
</span><span style="color: #008080;"> 3</span> 
<span style="color: #008080;"> 4</span>     <span style="color: #0000ff;">int</span><span style="color: #000000;"> new_n; 
</span><span style="color: #008080;"> 5</span>     <span style="color: #0000ff;">do</span><span style="color: #000000;">{
</span><span style="color: #008080;"> 6</span>         new_n = <span style="color: #800080;">0</span><span style="color: #000000;">;
</span><span style="color: #008080;"> 7</span>         <span style="color: #0000ff;">for</span>( <span style="color: #0000ff;">int</span> i = <span style="color: #800080;">1</span> ; i &lt; n ; i ++<span style="color: #000000;"> )
</span><span style="color: #008080;"> 8</span>             <span style="color: #0000ff;">if</span>( arr[i-<span style="color: #800080;">1</span>] &gt;<span style="color: #000000;"> arr[i] ){
</span><span style="color: #008080;"> 9</span>                 swap( arr[i-<span style="color: #800080;">1</span><span style="color: #000000;">] , arr[i] );
</span><span style="color: #008080;">10</span>                 new_n =<span style="color: #000000;"> i;
</span><span style="color: #008080;">11</span> <span style="color: #000000;">            }
</span><span style="color: #008080;">12</span>         n =<span style="color: #000000;"> new_n;
</span><span style="color: #008080;">13</span>     }<span style="color: #0000ff;">while</span>(new_n &gt; <span style="color: #800080;">0</span><span style="color: #000000;">);
</span><span style="color: #008080;">14</span> }</pre>
</div>
<p>&nbsp;</p>
<h3>1.5 相关性质</h3>
<ul>
<li>时间复杂度: O(n<sup>2</sup>)&nbsp;　</li>
<li>空间复杂度：O(1)</li>
<li>稳定排序　　　　　　</li>
<li>原地排序</li>
</ul>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2>2.选择排序（selection sort）</h2>
<h3>2.1 算法过程：</h3>
<p>　　首先在未排序的序列（通常就是整个序列）中找到最小的元素，来放到序列的头部；然后再从剩余的未排序的序列中寻找最小元素，放到有序序列的最尾端。</p>
<p>　　如此重复，直到整个序列都是有序的。</p>
<h3>2.2 可视化展示：</h3>
<p><img style="margin-left: 5%;" src="https://img2020.cnblogs.com/blog/1958859/202003/1958859-20200304181148041-261792818.gif" alt="" /></p>
<p>图源：<a href="https://juejin.im/post/5b4ef0bbe51d4519575a18d0">https://juejin.im/post/5b4ef0bbe51d4519575a18d0</a></p>
<h3>2.3 代码实现：　　</h3>
<p>&nbsp;python版本：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;"> 1</span> <span style="color: #0000ff;">def</span><span style="color: #000000;"> selection_sort(nums):
</span><span style="color: #008080;"> 2</span>     length =<span style="color: #000000;"> len(nums)
</span><span style="color: #008080;"> 3</span>     <span style="color: #0000ff;">if</span>(length==<span style="color: #000000;">0):
</span><span style="color: #008080;"> 4</span>         <span style="color: #0000ff;">return</span><span style="color: #000000;"> nums
</span><span style="color: #008080;"> 5</span>     <span style="color: #0000ff;">for</span> i <span style="color: #0000ff;">in</span><span style="color: #000000;"> range(length):
</span><span style="color: #008080;"> 6</span>         argmin =<span style="color: #000000;"> i
</span><span style="color: #008080;"> 7</span>         <span style="color: #0000ff;">for</span> j <span style="color: #0000ff;">in</span><span style="color: #000000;"> range(i,length):
</span><span style="color: #008080;"> 8</span>             <span style="color: #0000ff;">if</span>(nums[j]&lt;<span style="color: #000000;">nums[argmin]):
</span><span style="color: #008080;"> 9</span>                 argmin =<span style="color: #000000;"> j
</span><span style="color: #008080;">10</span>         nums[i],nums[argmin] =<span style="color: #000000;"> nums[argmin],nums[i]
</span><span style="color: #008080;">11</span>     <span style="color: #0000ff;">return</span> nums</pre>
</div>
<p>&nbsp;C++版本：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;"> 1</span> template&lt;typename T&gt;
<span style="color: #008080;"> 2</span> <span style="color: #0000ff;">void</span> selectionSort(T arr[], <span style="color: #0000ff;">int</span><span style="color: #000000;"> n){
</span><span style="color: #008080;"> 3</span> 
<span style="color: #008080;"> 4</span>     <span style="color: #0000ff;">for</span>(<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">0</span> ; i &lt; n ; i ++<span style="color: #000000;">){
</span><span style="color: #008080;"> 5</span> 
<span style="color: #008080;"> 6</span>         <span style="color: #0000ff;">int</span> minIndex =<span style="color: #000000;"> i;
</span><span style="color: #008080;"> 7</span>         <span style="color: #0000ff;">for</span>( <span style="color: #0000ff;">int</span> j = i + <span style="color: #800080;">1</span> ; j &lt; n ; j ++<span style="color: #000000;"> )
</span><span style="color: #008080;"> 8</span>             <span style="color: #0000ff;">if</span>( arr[j] &lt;<span style="color: #000000;"> arr[minIndex] )
</span><span style="color: #008080;"> 9</span>                 minIndex =<span style="color: #000000;"> j;
</span><span style="color: #008080;">10</span> 
<span style="color: #008080;">11</span> <span style="color: #000000;">        swap( arr[i] , arr[minIndex] );
</span><span style="color: #008080;">12</span> <span style="color: #000000;">    }
</span><span style="color: #008080;">13</span> }</pre>
</div>
<p>&nbsp;</p>
<h3>2.4 相关性质：</h3>
<ul>
<li>时间复杂度：O(n<sup>2</sup>)&nbsp; （无论什么数据都是，稳）</li>
<li>空间复杂度：O(1)</li>
<li>稳定性取决于具体实现方法</li>
<li>原地排序</li>
</ul>
<p>&nbsp;</p>
<h2>3.插入排序（insertion sort）</h2>
<h3>3.1 算法过程：</h3>
<p>　　将第一个元素看作是一个有序序列，第二个元素到最后一个元素看作是无序的。对于无序序列的每一个元素，放到有序序列的合适位置，变成新的有序序列，如此反复知道整个序列变成有序序列。（如果遇到相等元素的放在该元素的后面）</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; 通俗理解：类比拿到扑克牌时，拿到第一张扑克牌时，该扑克牌就是一个有序序列。每次取到一张新的扑克牌将其放在合适的位置，如此往复。</p>
<h3>3.2 可视化展示：</h3>
<p><img style="margin-left: 5%;" src="https://img2020.cnblogs.com/blog/1958859/202003/1958859-20200304180356384-1975292727.gif" alt="" /></p>
<p>&nbsp;　　图源：<a href="https://juejin.im/post/5b4ef681f265da0f4b7a8d44">https://juejin.im/post/5b4ef681f265da0f4b7a8d44</a></p>
<h3>&nbsp;3.3 代码实现：</h3>
<p>&nbsp;python版本：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;"> 1</span> <span style="color: #0000ff;">def</span><span style="color: #000000;"> insertion_sort(nums):
</span><span style="color: #008080;"> 2</span>     length =<span style="color: #000000;"> len(nums)
</span><span style="color: #008080;"> 3</span>     <span style="color: #0000ff;">if</span>(length==<span style="color: #000000;">0):
</span><span style="color: #008080;"> 4</span>         <span style="color: #0000ff;">return</span><span style="color: #000000;"> nums
</span><span style="color: #008080;"> 5</span>     <span style="color: #0000ff;">for</span> i <span style="color: #0000ff;">in</span><span style="color: #000000;"> range(length):
</span><span style="color: #008080;"> 6</span>         pre = i-1
<span style="color: #008080;"> 7</span>         cur_num =<span style="color: #000000;"> nums[i]
</span><span style="color: #008080;"> 8</span>         <span style="color: #0000ff;">while</span> pre&gt;=0 <span style="color: #0000ff;">and</span> nums[pre]&gt;<span style="color: #000000;">cur_num:
</span><span style="color: #008080;"> 9</span>             nums[pre+1] =<span style="color: #000000;"> nums[pre]
</span><span style="color: #008080;">10</span>             pre -= 1
<span style="color: #008080;">11</span>         nums[pre+1] = cur_num  <span style="color: #008000;">#</span><span style="color: #008000;"> 选择最后再交换这个元素</span>
<span style="color: #008080;">12</span>     <span style="color: #0000ff;">return</span> nums</pre>
</div>
<p>C++版本：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;"> 1</span> template&lt;typename T&gt;
<span style="color: #008080;"> 2</span> <span style="color: #0000ff;">void</span> insertionSort(T arr[], <span style="color: #0000ff;">int</span><span style="color: #000000;"> n) {
</span><span style="color: #008080;"> 3</span>     
<span style="color: #008080;"> 4</span>     <span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">1</span>; i &lt; n; i++<span style="color: #000000;">) {
</span><span style="color: #008080;"> 5</span>         <span style="color: #008000;">//</span><span style="color: #008000;">寻找元素arr[i]合适的插入位置</span>
<span style="color: #008080;"> 6</span>         <span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> j = i; j &gt; <span style="color: #800080;">0</span> &amp;&amp; arr[j] &lt; arr[j - <span style="color: #800080;">1</span>]; j--<span style="color: #000000;">) {
</span><span style="color: #008080;"> 7</span>             swap(arr[j], arr[j - <span style="color: #800080;">1</span><span style="color: #000000;">]);
</span><span style="color: #008080;"> 8</span> <span style="color: #000000;">        }
</span><span style="color: #008080;"> 9</span> <span style="color: #000000;">    }
</span><span style="color: #008080;">10</span> }</pre>
</div>
<p>&nbsp;</p>
<h3>3.4 算法改进：</h3>
<p>　　改进：先不进行swap，而是拷贝一份先前进行比较，找到合适的位置后再做赋值操作</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp;实现（C++）（上面python代码已经实现了）：</p>
<div class="cnblogs_code">
<pre>template&lt;typename T&gt;
<span style="color: #0000ff;">void</span> insertionSortImprove(T arr[], <span style="color: #0000ff;">int</span><span style="color: #000000;"> n) {

    </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">int</span> i = <span style="color: #800080;">1</span>; i &lt; n; i++<span style="color: #000000;">) {
        </span><span style="color: #008000;">//</span><span style="color: #008000;">寻找元素arr[i]合适的插入位置</span>
        T e =<span style="color: #000000;"> arr[i];
        </span><span style="color: #0000ff;">int</span><span style="color: #000000;"> j;
        </span><span style="color: #0000ff;">for</span> ( j = i; j &gt; <span style="color: #800080;">0</span> &amp;&amp; arr[j-<span style="color: #800080;">1</span>] &gt; e; j--<span style="color: #000000;">) {
            arr[j] </span>= arr[j - <span style="color: #800080;">1</span><span style="color: #000000;">];
        }
        arr[j] </span>=<span style="color: #000000;"> e;
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<h3>3.5 相关性质：　</h3>
<ul>
<li>时间复杂度：O(n<sup>2</sup>)&nbsp; &nbsp;最好的情况下是O(n),平均比较和移动次数约为 (n^2)/4</li>
</ul>
<p>　　（插入排序法的提前退出循环的特性，使得在面对一个有序性强的数组时，性能非常优异）</p>
<p>　　（插入排序法理论上来说可以提前跳出循环，速度应该快于选择排序法，但由于多次交换的赋值操作使得时间变长。这说明算法实际的运行速度还受限于实现方式，例如递归时开辟栈空间的开销，交换操作的开销等等）</p>
<ul>
<li>空间复杂度：O(1)</li>
<li>稳定排序</li>
<li>原地排序</li>
</ul>
<p>&nbsp;</p>
<h2>4.插入排序的衍生算法--希尔排序</h2>
<p>1959年Shell发明，第一个突破O(n<sup>2</sup>)的排序算法</p>
<p>插入排序在对几乎已经排好序的数据操作时，效率高，即可以达到线性排序的效率。但插入排序一般来说是低效的，因为插入排序每次只能将数据移动一位，因此如果一次可以移动多位，也就是有一个间隔，就有了希尔排序的思路。</p>
<h3>4.1 算法过程</h3>
<p>　　基本思想：先将整个待排序的序列分割成为若干子序列分别进行插入排序，等到整个序列中基本有序时，再对整个序列进行插入排序。</p>
<p>　　具体过程：</p>
<div><ol class="_mce_tagged_br">
<li>
<p>选择一个增量序列 t1，t2，&hellip;&hellip;，tk，其中 ti &gt; tj, tk = 1；</p>
</li>
<li>
<p>按增量序列个数 k，对序列进行 k 趟排序；</p>
</li>
<li>
<p>每趟排序，根据对应的增量 ti，将待排序列分割成若干长度为 m 的子序列，分别对各子表进行直接插入排序。仅增量因子为 1 时，整个序列作为一个表来处理，表长度即为整个序列的长度。</p>
</li>
</ol>
<p>&nbsp; &nbsp; &nbsp; &nbsp; 来张图帮助理解：</p>
<p>&nbsp;&nbsp;<img src="https://img2020.cnblogs.com/i-beta/1958859/202003/1958859-20200304175033602-1483264059.png" alt="" /></p>
<p>&nbsp;</p>
<p>　　图源：<a href="https://www.cnblogs.com/chengxiao/p/6104371.html">https://www.cnblogs.com/chengxiao/p/6104371.html</a></p>
<p>&nbsp;</p>
<h3>4.2 可视化展示：</h3>
<p>&nbsp;<img src="https://img2020.cnblogs.com/blog/1958859/202003/1958859-20200304181647841-1047668845.gif" alt="" /></p>
<p>图源：<a href="https://juejin.im/post/5bf9f2285188256b0f5832a0">https://juejin.im/post/5bf9f2285188256b0f5832a0</a></p>
<p>&nbsp;</p>
<h3>4.3 代码实现：</h3>
<p>　　由于原始的希尔增量序列不互质，可能会出现增量序列不起作用的情况，故在此不使用希尔增量序列。</p>
<p>&nbsp;python版本：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;"> 1</span> <span style="color: #0000ff;">import</span><span style="color: #000000;"> math #使用math.floor()来对增量进行取整
</span><span style="color: #008080;"> 2</span> <span style="color: #0000ff;">def</span><span style="color: #000000;"> shell_sort(nums):
</span><span style="color: #008080;"> 3</span>     length =<span style="color: #000000;"> len(nums)
</span><span style="color: #008080;"> 4</span>     <span style="color: #0000ff;">if</span>(length==<span style="color: #000000;">0):
</span><span style="color: #008080;"> 5</span>         <span style="color: #0000ff;">return</span><span style="color: #000000;"> nums
</span><span style="color: #008080;"> 6</span>     offset = 1
<span style="color: #008080;"> 7</span>     <span style="color: #0000ff;">while</span>(offset&lt;length/3<span style="color: #000000;">):
</span><span style="color: #008080;"> 8</span>         offset = offset*3 + 1
<span style="color: #008080;"> 9</span>     <span style="color: #0000ff;">while</span> offset&gt;<span style="color: #000000;">0:
</span><span style="color: #008080;">10</span>         <span style="color: #0000ff;">for</span> i <span style="color: #0000ff;">in</span><span style="color: #000000;"> range(offset,length):
</span><span style="color: #008080;">11</span>             tmp =<span style="color: #000000;"> nums[i]
</span><span style="color: #008080;">12</span>             j = i-<span style="color: #000000;">offset
</span><span style="color: #008080;">13</span>             <span style="color: #0000ff;">while</span> j&gt;=0 <span style="color: #0000ff;">and</span> nums[j] &gt;<span style="color: #000000;"> tmp:
</span><span style="color: #008080;">14</span>                 nums[j+offset] =<span style="color: #000000;"> nums[j]
</span><span style="color: #008080;">15</span>                 j -=<span style="color: #000000;"> offset
</span><span style="color: #008080;">16</span>             nums[j+offset] =<span style="color: #000000;"> tmp
</span><span style="color: #008080;">17</span>         offset = math.floor(offset/3<span style="color: #000000;">)
</span><span style="color: #008080;">18</span>     <span style="color: #0000ff;">return</span> nums</pre>
</div>
<p>&nbsp; C++版本：</p>
<div class="cnblogs_code">
<pre><span style="color: #008080;"> 1</span> template&lt;typename T&gt;
<span style="color: #008080;"> 2</span> <span style="color: #0000ff;">void</span> shellSort(T arr[], <span style="color: #0000ff;">int</span><span style="color: #000000;"> n){
</span><span style="color: #008080;"> 3</span> 
<span style="color: #008080;"> 4</span>     <span style="color: #008000;">//</span><span style="color: #008000;"> 计算增量序列: 1, 4, 13, 40, 121, 364, 1093...</span>
<span style="color: #008080;"> 5</span>     <span style="color: #0000ff;">int</span> offset = <span style="color: #800080;">1</span><span style="color: #000000;">;
</span><span style="color: #008080;"> 6</span>     <span style="color: #0000ff;">while</span>( offset &lt; n/<span style="color: #800080;">3</span><span style="color: #000000;"> )
</span><span style="color: #008080;"> 7</span>         offset = <span style="color: #800080;">3</span> * offset + <span style="color: #800080;">1</span><span style="color: #000000;">;
</span><span style="color: #008080;"> 8</span> 
<span style="color: #008080;"> 9</span>     <span style="color: #0000ff;">while</span>( offset &gt;= <span style="color: #800080;">1</span><span style="color: #000000;"> ){
</span><span style="color: #008080;">10</span> 
<span style="color: #008080;">11</span>         <span style="color: #0000ff;">for</span>( <span style="color: #0000ff;">int</span> i = offset ; i &lt; n ; i ++<span style="color: #000000;"> ){
</span><span style="color: #008080;">12</span> 
<span style="color: #008080;">13</span>             <span style="color: #008000;">//</span><span style="color: #008000;"> 对 arr[i], arr[i-offset ], arr[i-2*offset ], arr[i-3*offset ]... 使用插入排序</span>
<span style="color: #008080;">14</span>             T e =<span style="color: #000000;"> arr[i];
</span><span style="color: #008080;">15</span>             <span style="color: #0000ff;">int</span><span style="color: #000000;"> j;
</span><span style="color: #008080;">16</span>             <span style="color: #0000ff;">for</span>( j = i ; j &gt;= offset &amp;&amp; e &lt; arr[j-offset ] ; j -=<span style="color: #000000;"> offset )
</span><span style="color: #008080;">17</span>                 arr[j] = arr[j-<span style="color: #000000;">offset ];
</span><span style="color: #008080;">18</span>             arr[j] =<span style="color: #000000;"> e;
</span><span style="color: #008080;">19</span> <span style="color: #000000;">        }
</span><span style="color: #008080;">20</span> 
<span style="color: #008080;">21</span>         offset /= <span style="color: #800080;">3</span><span style="color: #000000;">;
</span><span style="color: #008080;">22</span> <span style="color: #000000;">    }
</span><span style="color: #008080;">23</span> }</pre>
</div>
<h3>4.4 希尔排序的增量序列：</h3>
<ul>
<li>shell 增量序列 ： k = k/2</li>
<li>Hibbard增量序列：Dk = 2^k-1 相邻元素互质</li>
<li>Sedgewick增量序列：9*4^i - 9*2^i +1 或 4^i - 3*2^i +1</li>
<li><a href="https://blog.csdn.net/Foliciatarier/article/details/53891144" target="_blank">更多的增量序列以及代码实现</a></li>
</ul>
<h3>4.5 相关性质：</h3>
<ul>
<li>时间复杂度：希尔排序的复杂度与增量序列的选择有关。具体分析可以参考：
<p class="_1RuRku"><a href="https://www.jianshu.com/p/d730ae586cf3" target="_blank">排序：希尔排序（算法）</a></p>
</li>
<li>空间复杂度： O(1)&nbsp;</li>
<li>不稳定排序</li>
<li>原地排序</li>
</ul>
<p>&nbsp;</p>
<p>END</p>
</div>
