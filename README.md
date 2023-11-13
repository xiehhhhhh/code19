# code19
//贪心区间覆盖
#include<cmath>
#include<iostream>
#include<algorithm>
using namespace std;
struct Point
{
	double x;
	double y;
}point[1000];
 
int cmp(const void *a, const void *b)
{
    return (*(Point *)a).x>(*(Point *)b).x?1:-1;
}
 
int main()
{
	int n,d;
	int num=1;
	while(cin>>n>>d)
	{
		int counting=1;
		if(n==0&&d==0) break;
		for(int i=0;i<n;i++)
		{
			int x,y;
			cin>>x>>y;
			if(y>d)
			{
				counting=-1;
			}
			double t=sqrt(d*d-y*y);
			//转化为最少区间的问题 
			point[i].x=x-t;
			//区间左端点 
			point[i].y=x+t;
			//区间右端点 
		}
		if(counting!=-1)
		{
			qsort(point,n,sizeof(point[0]),cmp);
			//按区间左端点排序 
			double s=point[0].y;
			//区间右端点 
			for(int i=1;i<n;i++)
			{
				if(point[i].x>s)
				//如果两个区间没有重合,增加雷达数目并更新右端点 
				{
					counting++;
					s=point[i].y; 
				}
				else if(point[i].y<s)
				//如果第二个区间被完全包含于第一个区间,更新右端点 
				{
					s=point[i].y;
				}
			}
		}
		cout<<"Case "<<num<<':'<<' '<<counting<<endl;
		num++; 
	}
}	
