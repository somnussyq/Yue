<img src=http://chuantu.biz/t6/187/1514299017x-1404764539.png />

**Founder**: [@Coder-Yu ](https://github.com/Coder-Yu)<br>

<h2>Introduction</h2>

**Yue** is a Python library for Music Recommendation (Python 2.7.x). It implements a suit of state-of-the-art recommendations. To run Yue easily (no need to setup dendencies used in RecQ one by one), the leading open data science platform  [**Anaconda**](https://www.continuum.io/downloads) is strongly recommended. It integrates Python interpreter, common scientific computing libraries (such as Numpy, Pandas, and Matplotlib), and package manager, all of them make it a perfect tool for data science researcher.


<h2>Features</h2>
<ul>
<li><b>Cross-platform</b>: as a Python software, Yue can be easily deployed and executed in any platforms, including MS Windows, Linux and Mac OS.</li>
<li><b>Fast execution</b>: Yue is based on the fast scientific computing libraries such as Numpy and some light common data structures, which make it run much faster than other libraries based on Python.</li>
<li><b>Easy configuration</b>: Yue configs recommenders using a configuration file.</li>
<li><b>Easy expansion</b>: Yue provides a set of well-designed recommendation interfaces by which new algorithms can be easily implemented.</li>
</ul>

<h2>How to Run it</h2>
<ul>
<li>1.Configure the **xx.conf** file in the directory named config. (xx is the name of the algorithm you want to run)</li>
<li>2.Run the **main.py** in the project, and then input following the prompt.</li>
</ul>
<h2>How to Configure it</h2>
<h3>Essential Options</h3>
<div>
 <table class="table table-hover table-bordered">
  <tr>
    <th width="12%" scope="col"> Entry</th>
    <th width="16%" class="conf" scope="col">Example</th>
    <th width="72%" class="conf" scope="col">Description</th>
  </tr>
  <tr>
    <td>record</td>
    <td>D:/xiami/100K.txt</td>
    <td>Set the path to input dataset.</td>
  </tr> 
  <tr>
    <td scope="row">record.setup</td>
    <td>-columns user:0,track:1,artist:2,album:3 -delim ,</td>
    <td>-columns: this option specifies what colums in the dataset mean. Four types of entities supported. If some types of information are missing, just skip the corresponding type;</br> -delim: this option specifies which symbol separates the columns.       
    </td>
  </tr>
  <tr>
    <td scope="row">recommender</td>
    <td>UserKNN/ItemKNN/MostPop/etc.</td>
    <td>the name of the recommender</br>
    </td>
  </tr>
  <tr>
    <td scope="row">evaluation.setup</td>
    <td>-testSet ../dataset/testset.txt</td>
    <td>Main option: -testSet, -ap, -cv -byTime</br>
      -testSet path/to/test/file   (need to specify the test set manually)</br>
      -ap ratio   (ap means that the ratings are automatically partitioned into training set and test set, the number is the ratio of test set. e.g. -ap 0.2)</br>
      -cv k   (-cv means cross validation, k is the number of the fold. e.g. -cv 5)</br>
      <b>-byTime ratio </b> (sort the user record in order of the time. ratio decides the percentage of test set(recently played).</br>
      Secondary option:-b, -p, -cold</br>
      <b>-target track </b>(This option decides which type of object will be recommended (artist, track, album). Only available for some general recommenders like MostPop) </br> 
      -b val （binarizing the rating values. Ratings equal or greater than val will be changed into 1, and ratings lower than val will be changed into 0. e.g. -b 3.0）</br>
      -p (if this option is added, the cross validation wll be excuted parallelly, otherwise excuted one by one) </br>
      -cold threshold (evaluation on cold-start users, users in training set with ratings more than threshold will be removed from the test set)
     </td>
  </tr>
  <tr>
    <td scope="row">item.ranking</td>
    <td>off -topN 5,10,20 </td>
    <td>-topN N1,N2,N3...: the length of the recommendation list. *Yue can generate multiple evaluation results for different N at the same time</br>
    </td>
  </tr>
  <tr>
    <td scope="row">output.setup</td>
    <td>on -dir ./Results/</td>
    <td>Main option: whether to output recommendation results</br>
      -dir path: the directory path of output results.
       </td>
  </tr>  
  </table>
</div>


<h3>Model-based Options</h3>
<div>
 <table class="table table-hover table-bordered">
  <tr>
    <td scope="row">num.factors</td>
    <td>5/10/20/number</td>
    <td>Set the number of latent factors</td>
  </tr>
  <tr>
    <td scope="row">num.max.iter</td>
    <td>100/200/number</td>
    <td>Set the maximum number of iterations for iterative recommendation algorithms. </td>
  </tr>
  <tr>
    <td scope="row">learnRate</td>
    <td>-init 0.01 -max 1</td>
    <td>-init initial learning rate for iterative recommendation algorithms; <br>
      -max: maximum learning rate (default 1);<br>
    </td>
  </tr>
  <tr>
    <td scope="row">reg.lambda</td>
    <td>-u 0.05 -i 0.05 -b 0.1</td>
    <td>
      -u: user regularizaiton; -i: item regularization; -b: bias regularizaiton;</td>
  </tr> 
  </table>
</div>

<h2>How to extend it</h2>
<ul>
<li>1.Make your new algorithm generalize the proper base class.</li>
<li>2.Rewrite some of the following functions as needed.</li>
</ul>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- readConfiguration()<br>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- printAlgorConfig()<br>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- initModel()<br>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- buildModel()<br>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- saveModel()<br>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- loadModel()<br>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- predict()<br>

<h2>Algorithms Implemented</h2>
<p><b>Note: </b>We use SGD to obtain the local minimum. So, there have some differences between the original papers and the code in terms of fomula presentation. If you have problems in understanding the code, please open an issue to ask for help. We can guarantee that all the implementations are carefully reviewed and tested. </p> 
<div>

  <table class="table table-hover table-bordered">
  <tr>
		<th>Item Ranking</th>
		<th>Paper</th>
  </tr>
  <tr>
    <td scope="row">Rand</td>
    <td>Recommend tracks, artists or albums randomly
     </td>
  </tr>
  <tr>
    <td scope="row">MostPop</td>
    <td>Recommend most popular tracks, artists or albums
     </td>
  </tr>
    <tr>
	<td scope="row">BPR</td>
    <td>Rendle et al., BPR: Bayesian Personalized Ranking from Implicit Feedback, UAI 2009.<br>
    </td>
  </tr>  

  <tr>
    <td scope="row">MEM(implementing...)</td>
    <td>Wang et al., Learning music embedding with metadata for context aware recommendation, ICMR 2016.
     </td>
  </tr>  
   <tr>
    <td scope="row">FISM</td>
    <td>Kabbur et al., FISM: Factored Item Similarity Models for Top-N Recommender Systems, KDD 2013.
     </td>
  </tr>
    <tr>
    <td scope="row">IPF (*Removed, not suitable for the music recommendation)</td>
    <td>Xiang et al., Temporal Recommendation on Graphs via Long- and Short-term Preference Fusion, KDD 2010.
     </td>
  </tr>
    <tr>
    <td scope="row">WRMF</td>
    <td>Hu et al., Collaborative Filtering for Implicit Feedback Datasets, KDD 2009.
     </td>
  </tr>
  </table>
</div>

</br>
<h3>Dataset</h3>
<div>
 <table class="table table-hover table-bordered">
  <tr>
    <th rowspan="2" scope="col">Data Set</th>
    <th colspan="5" scope="col" class="text-center">Basic Meta</th>
    <th colspan="3" scope="col" class="text-center">Context</th> 
    </tr>
  <tr>
    <th class="text-center">Users</th>
    <th class="text-center">Tracks</th>
    <th class="text-center">Artists</th>    
    <th class="text-center">Albums</th>
   <th class="text-center">Record</th>
    <th class="text-center">Tag</th>
    <th class="text-center">User Profile</th>
   <th class="text-center">Artist Profile</th>
    </tr> 
  <tr>
    <td><a href="https://pan.baidu.com/s/1slr64rj" target="_blank"><b>NowPlaying</b></a> [1]</td>
    <td>1,744</td>
    <td>16,864</td>
    <td>2,108</td>
   <td>N/A</td>
    <td>1,117,335</td>
    <td>N/A</td>
    <td>N/A</td>
    <td>N/A</td>
    </tr>  
   <tr>
    <td><a href="https://pan.baidu.com/s/1dEBXClV" target="_blank"><b>Xiami</b></a> [2]</td>
    <td>4,270</td>
    <td>177,289</td>
    <td>25,844</td>
   <td>68,479</td>
    <td>1,337,948</td>
    <td>N/A</td>
    <td>N/A</td>
    <td>N/A</td>
   </tr>  
  </table>
</div>

<h3> Dataset Reference </h3>
<p> [1]. Eva Zangerle, Martin Pichl, Wolfgang Gassler, and Günther Specht. 2014. #nowplaying Music Dataset: Extracting Listening Behavior from Twitter. In Proceedings of the First International Workshop on Internet-Scale Multimedia Management (WISMM '14). ACM, New York, NY, USA, 21-26 </p>
<p> [2]. Wang, Dongjing, et al. "Learning music embedding with metadata for context aware recommendation." Proceedings of the 2016 ACM on International Conference on Multimedia Retrieval. ACM, 2016.</p>

