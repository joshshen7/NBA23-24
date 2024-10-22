# NBA23-24

import matplotlib.pyplot as plt
import pandas as pd 
myNBA = pd.read_csv('C:/INFS 6351/nba.csv')
head = myNBA.head()
print(head)
df = pd.DataFrame(myNBA)
print(df)

fig1 = plt.figure(1)
ax = fig1.add_subplot(1,1,1)
ax.hist(myNBA['PPG'], bins = 5)
ax.set_title('PPG vs 3PTA Histogram')
ax.set_xlabel('PPG')
ax.set_ylabel('3PTA')

fig2 = plt.figure(2)
ax2 = fig2.add_subplot(1,1,1)
ax2.boxplot(myNBA['PPG'])
ax2.set_xlabel('Points Per Game')
ax2.set_title('PPG Boxplot')

fig3 = plt.figure(3)
ax3 = fig3.add_subplot(1,1,1)
var = myNBA.groupby('Position').PPG.mean()
print(var)
ax3.set_xlabel('Position')
ax3.set_ylabel('Average PPG')
ax3.set_title('Position vs. Average PPG Bar Chart')
var.plot(kind = 'bar')

fig4 = plt.figure(4, figsize = (12,6))
ax4 = fig4.add_subplot(1,2,1)
ax4.scatter(myNBA['PPG'],myNBA['FG%'])
ax4.set_title('PPG by FG% Scatter Plot')
ax4.set_xlabel('PPG')
ax4.set_ylabel('FG%')

ax5 = fig4.add_subplot(1,2,2)
ax5.scatter(myNBA['3pt %'], myNBA['FG%'], s = myNBA['GP'])
ax5.set_title('3pt% by FG%\nBubble Size = Games Played')
ax5.set_xlabel('3pt%')
ax5.set_ylabel('FG%')

fig5 = plt.figure(5)
ax6 = fig5.add_subplot(1,1,1)
new = myNBA.groupby(['Position']).Position.count()
new.plot.pie(y = new.index, labels = list(new), autopct='%1.1f%%', shadow = True, colors = ['red', 'blue', 'yellow'], explode = (0.5,0,0), startangle = 45)
ax6.set_title('Top 30 NBA Scorers by Position %')
plt.legend(new.keys())
plt.axis('equal')
plt.tight_layout()

plt.show()
