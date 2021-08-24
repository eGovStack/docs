# DIGIT: Internal Datamart Deployment Steps

Steps for setting up the environment and running the script file to get a fresh copy of the required Datamart CSV file.

### Steps for setting up the environment for running the script  <a id="Steps-for-setting-up-the-environment-for-running-the-script"></a>

**\(One Time Setup\)**

1. **Install Kubectl** Step 1: Go through the Kubernetes documentation page to install and configure the kubectl. Following are useful links:  [Kubernetes Installation Doc](https://kubernetes.io/docs/tasks/tools/install-kubectl/)  [Kubernetes Ubuntu Installation](https://matthewpalmer.net/kubernetes-app-developer/articles/install-kubernetes-ubuntu-tutorial.html)

After installing type the below command to check the version install in your system`1 kubectl version`

 Step 2: Install aws-iam-authenticator  
[![](https://docs.aws.amazon.com/assets/images/favicon.ico)Installing aws-iam-authenticator - Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html)

 Step 3: After installing, you need access to a particular environment cluster.

* Go to $HOME/.Kube folder 

`1cd 2cd .kube`

 Open the config file and replace the content with the environment cluster config file. \(Config file will be attached\)`1gedit config`

* Copy-paste the content from the config file provided to this config file opened and save the file.

**2. Exec into the pod**`1kubectl exec --stdin --tty playground-584d866dcc-cr5zf -n playground -- /bin/bash`

\(_Replace the pod name depending on what data you want._

_Refer to Table 1.2 for more information_\)

**3. Install Python and check to see if it installed correctly**`1apt install python3.8 2python --version`

**4. Install pip and check to see if it installed correctly**`1apt install python3-pip 2pip3 --version`

**5. Install psycopg2 and Pandas**`1pip3 install psycopg2-binary pandas`

Note: If this doesn’t work then try this command`1pip3 install --upgrade pip`

and running the \#5 command again

### **Steps for setting up the environment for running the script**  <a id="Steps-for-setting-up-the-environment-for-running-the-script.1"></a>

**\(Every time you want a datamart with the latest data available in the pods\)**

**1. Sending the python script to the pod**`1tar cf - /home/priyanka/Desktop/mcollect.py | kubectl exec -i -n playground playground-584d866dcc-cr5zf -- tar xf - -C /tmp`

Note: Replace the file path \(/home/priyanka/Desktop/mcollect.py\) with your own file path \(/home/user\_name/Desktop/script\_name.py\)

Note: Replace the pod name depending on what data you want.  

\(Refer to Table 1.2 for more information on pod names\)

**2. Exec into the pod**`1kubectl exec --stdin --tty playground-584d866dcc-cr5zf -n playground -- /bin/bash`

\(Note: Replace the pod name depending on what data you want.`1kubectl exec --stdin --tty <your_pod_name> -n playground -- /bin/bash`

 Refer to Table 1.2 for more information\)

  
**3. Move into tmp directory and then move into the directory your script was in**`1cd tmp 2cd home/priyanka/Desktop`

for example :`1cd home/<your_username>/Desktop`

**4. List the files there**`1ls`

\(Python script file should be present here\)

\(Refer Table 1.1 for the list of script file names for each module\)

**5. Run the python script file**`1python3 ws.py`

\(name of the python script file will change depending on the module\)

\(Refer Table 1.1 for the list of script file names for each module\)

**6. Outside the pod shell, In your home directory run this command to copy the CSV file/files to your desired location**`1kubectl cp playground/playground-584d866dcc-cr5zf:/tmp/mcollectDatamart.csv /home/priyanka/Desktop/mcollectDatamart.csv`

\(The list of CSV file names for each module will be mentioned below\)

  
**7. The reported CSV file is ready to use.**

### Jupyter vs Excel for Data Analysis <a id="Jupyter-vs-Excel-for-Data-Analysis"></a>

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Jupyter</b>
      </th>
      <th style="text-align:left"><b>Excel</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>Using jupyter will be <b>command-based</b>.</p>
        <p>Will take some time getting used to it.</p>
      </td>
      <td style="text-align:left"><b>Ease of Use</b> with the Graphical User Interface (<b>GUI</b>). Learning
        formulas is fairly easier.</td>
    </tr>
    <tr>
      <td style="text-align:left">Jupyter requires python language for data analysis hence a <b>steeper learning curve.</b>
      </td>
      <td style="text-align:left"><b>Negligible</b> previous knowledge is required.</td>
    </tr>
    <tr>
      <td style="text-align:left">Equipped to handle lots of data really <b>quickly</b>. With the bonus of
        ease of <b>accessibility to databases</b> like Postgres and Mysql where actual
        data is stored.</td>
      <td style="text-align:left">
        <p>Excel can only handle so much data. Scalability becomes difficult and
          messy.</p>
        <p><b>More Data = Slower Results</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>Summary:</b>
        </p>
        <p>Python is harder to learn because you have to download many packages and
          set the correct development environment on your computer. However, it provides
          a big leg up when working with big data and creating repeatable, automatable
          analyses, and in-depth visualizations.</p>
      </td>
      <td style="text-align:left">
        <p><b>Summary:</b>
        </p>
        <p>Excel is best when doing small and one-time analyses or creating basic
          visualizations quickly. It is easy to become an intermediate user relatively
          without too much experience dueo its GUI.</p>
      </td>
    </tr>
  </tbody>
</table>

#### How to install and configure jupyter to analyze the datamart <a id="How-to-install-and-configure-jupyter-to-analyze-the-datamart"></a>

Watch this video

[![](https://www.youtube.com/s/desktop/65defdc1/img/favicon_144x144.png)How To Install Jupyter Notebook In Ubuntu Linux](https://www.youtube.com/watch?v=Yg9AkozItTU)

OR

Follow these steps -&gt;

**\(One Time Setup\)**

1. **Install Python and check to see if it installed correctly**

`1apt install python3.8 2python --version`

  
2. **Install pip and check to see if it installed correctly**`1apt install python3-pip 2pip3 --version`

**3. Install jupyter**`1pip3 install notebook`

**\(Whenever you want to run Jupyter lab\)**

1. **To run jupyter lab**

`1jupyter notebook`

 **2.** **To open a new notebook**

New -&gt; Python3 notebook

**3. To open an existing notebook**

Select File -&gt; Open

Go to the directory where your sample notebook is.

Select that notebook \(Ex: sample.pynb\)

**Opening an existing notebook**

![](../../../.gitbook/assets/image%20%28285%29.png)

After opening

![](../../../.gitbook/assets/image%20%28283%29.png)

### Table 1.1 - File Names for each Module <a id="Table-1.1---File-Names-for-each-Module"></a>

| **Module Name** | **Script File Name \(With Links\)** | **Datamart CSV File Name** | **Datamart CSV File Name** |
| :--- | :--- | :--- | :--- |
| **PT** | [pt.py](https://github.com/egovernments/utilities/blob/Rain-3035/datamart/property-tax/pt.py) | ptDatamart.csv |  |
| **W&S** | [ws.py](https://github.com/egovernments/utilities/blob/Rain-3035/datamart/water-and-sewerage/ws.py) | waterDatamart.csv | sewerageDatamart.csv |
| **PGR** | [pgr.py](https://github.com/egovernments/utilities/blob/Rain-3035/datamart/pgr/pgr.py) | pgrDatamart.csv |  |
| **mCollect** | [mcollect.py](https://github.com/egovernments/utilities/blob/Rain-3035/datamart/mcollect/mcollect.py) | mcollectDatamart.csv |  |
| **TL** | [tl.py](https://github.com/egovernments/utilities/blob/Rain-3035/datamart/trade-license/tl.py) | tlDatamart.csv | tlrenewDatamart.csv |
| **Fire Noc** | [fn.py](https://github.com/egovernments/utilities/blob/Rain-3035/datamart/firenoc/fn.py) | fnDatamart.csv |  |
| **OBPS \(Bpa\)** | [bpa.py](https://github.com/egovernments/utilities/tree/Rain-3035/datamart/obps/bpa)   | bpaDatamart.csv   |  |

### Table 1.2 - Pod Names for each Module <a id="Table-1.2---Pod-Names-for-each-Module"></a>

| **Module Name** | **Pod Name** | **Description** |
| :--- | :--- | :--- |
| **PT** | playground-865db67c64-tfdrk | Punjab Prod Data in UAT Environment |
| **W&S** | playground-584d866dcc-cr5zf | QA Data |
| **PGR** | Local Data  | Data Dump  |
| **mCollect** | playground-584d866dcc-cr5zf | QA Data |
| **TL** | playground-584d866dcc-cr5zf | QA Data |
| **Fire Noc** | playground-584d866dcc-cr5zf | QA Data |
| **OBPS \(Bpa\)** | playground-584d866dcc-cr5zf | QA Data |







> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

