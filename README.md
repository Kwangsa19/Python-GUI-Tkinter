# Python-GUI-Tkinter

>Please ensure that you have the latest version of Python. If not, then please download [here](https://www.python.org/downloads/).

>Ensure you have all the following modules or sub-modules (Some of them require manual installation):
>tkinter, plotdata, stats, matplotlib, regression plot, seaborn, pandas, pylot.
>After installing Python, open your terminal or cmd, type this command: pip install "module" (Replace the module with the above. Note that not every one of them is a module). 

## Description 

This is based on the Coursera Project Course Work, "Build a Python GUI with Tkinter" (Please enroll to this course by visiting this [link](https://www.coursera.org/projects/build-a-python-gui-with-tkinter)). This course demonstrates how to create a visual interface using Python and determine the correlation between temperature and rain, and birth of month and number of births. <br>

Tkinter application inherits from Frame to create the Graphical User Interface (GUI) Window. It is a container widget that groups and organizes other wides within a GUI. The purpose of it is to create visual structure and layot, separate different sections of the interface, manage complex layouts more effectively. In practical ways, we can group the following: 
* Related widgets (buttons, labels, entry fields, etc.).
* Create tabbed interfaces with multiple frames.
* Implement master-detail views.

dataview.py: 
* It starts from importing tkinter and some modueles from other files, such as plotdata, regression_plot, stats, and stats_column.
  ```
  from tkinter import *
  from tkinter.ttk import *

  from plotdata import regression_plot
  from stats import stats_columns
  ```
* There are four functions in a class application. They are Init, widgets, show_graph, show_stats.
   ```
   # initialize the attributes of an object as soon as the object is formed. 
   # "Self" is always passed in its argument, representing the object of the class itself. 
   def __init__(self, master=None): 
        super().__init__(master)
        self.master = master
        self.create_widgets()

  def create_widgets(self):
        self.winfo_toplevel().title("Data View")
        self.l1 = Label(self.master, text="File Name")
        self.l2 = Label(self.master, text="X Label")
        self.l3 = Label(self.master, text ="Y Label")
   # see the rest in a file. Widgets and interface buttons. 

   def show_graph(self):
        regression_plot(self.eFname.get(), self.eX.get(), self.eY.get()) # Show the regression plots
        
    def show_stats(self):
        xstats, ystats = stats_columns(self.eFname.get(), self.eX.get(), self.eY.get())
        self.txtX.insert(INSERT,xstats)
        self.txtY.insert(INSERT,ystats)
   # Show stats 
   ```
plotdata.py: 
* It starts from importing some modules from pandas, matplotlib, pyplot, seaborn
  ```
  import pandas as pd
  from  matplotlib import pyplot as plt
  import matplotlib
  import seaborn as sns
  ```
* There is one function (Regression_plot) to read the file CSV and plot variables X and Y.
  ```
  def regression_plot(filename, xlabel, ylabel):
    # create the dataframe using the csv file upload
    df = pd.read_csv(filename)
    # Temp, Year and Rain(fall)
    # How we set width, height using matplotlib settings
    sns.set(rc={'figure.figsize':(12,6)})
    sns.regplot(x=xlabel, y=ylabel, data=df)
    # regression line shows a possible positive correlation - as temp increases so does rainfall.
    plt.show()
    return
  ```
* There are two declarations on conditions:
  ```
  if __name__ == '__main__':
    regression_plot('tempRainYearly.csv','Temp', 'Rain' ) # for Temperature and rain

  if __name__ == '__main__':
    regression_plot('birthYearly.csv','month', 'births' ) # for month of births and births
  ```
stats.py:
* It starts from importing pandas. 
  ```
  import pandas as pd
  ```
* There is one function.
  ```
  def stats_columns(filename, xlabel, ylabel):
    df = pd.read_csv(filename)

    xdata = df[xlabel]
    ydata = df[ylabel]

    xstats = xdata.describe()
    ystats = ydata.describe()
    
    return xstats, ystats
  ```
* There are two declarations on conditions:
  ```
  if __name__ == '__main__':
    print (stats_columns('tempRainYearly.csv','Temp', 'Rain' )) # for Temperature and rain

  if __name__ == '__main__':
    print (stats_columns('birthYearly.csv','month', 'births' )) # for month of births and births
  ```
  
## Implementation

1. Download this repository.
2. Run dataview.py using Visual Studio Code or Python latest version.
3. The interface will prompt you options to type the name of the file, determine the X Label and Y Label, or quit.
4. The following are the correlation between the birth months and the number of births. 

![BirthlyYear Stats](https://github.com/Kwangsa19/Python-GUI-Tkinter/assets/135963482/7de8e850-7ff5-459c-aff7-cf84ee693163)

![BirthlyYear Plot](https://github.com/Kwangsa19/Python-GUI-Tkinter/assets/135963482/91f46c45-66df-4b84-8e62-527aec6793f8)  


<br>

5. The following are the correlation between the temperature and rain.

![tempRainYearly Stats](https://github.com/Kwangsa19/Python-GUI-Tkinter/assets/135963482/cc6fabb1-d6f7-41b2-91bd-3e0f608fdc0a)  

![tempRainYearly Plot](https://github.com/Kwangsa19/Python-GUI-Tkinter/assets/135963482/ad1662c8-7316-40c3-b8ea-c59ef50be073)

6. You can also downlaod the figures, adjust the size, and zoom the figures.

## Future Works
* More math formula samples.
* Many formats (not just csv).
* Using "input" to allow users choose the files regardless of the location path.  
