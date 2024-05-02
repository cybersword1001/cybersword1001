- 👋 Hi, I’m @cybersword1001
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
cybersword1001/cybersword1001 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
//practical no 4
#include <stdio.h>
#include <stdlib.h> // Include this for system("cls") or system("clear")
int main()
{
    int p[20], bt[20], pri[20], wt[20], tat[20], i, k, n, temp;
    float wtavg, tatavg;
    system("cls"); // Clear the screen

    printf("Enter the number of processes: ");
    scanf("%d", &n);
    for (i = 0; i < n; i++)
    {
        p[i] = i;
        printf("Enter the Burst Time & Priority of Process %d: ", i);
        scanf("%d %d", &bt[i], &pri[i]);
    }

    for (i = 0; i < n; i++)
        for (k = i + 1; k < n; k++)
            if (pri[i] > pri[k])
            {
                temp = p[i];
                p[i] = p[k];
                p[k] = temp;
                temp = bt[i];
                bt[i] = bt[k];
                bt[k] = temp;
                temp = pri[i];
                pri[i] = pri[k];
                pri[k] = temp;
            }

    wtavg = wt[0] = 0;
    tatavg = tat[0] = bt[0];
    for (i = 1; i < n; i++)
    {
        wt[i] = wt[i - 1] + bt[i - 1];
        tat[i] = tat[i - 1] + bt[i];

        wtavg = wtavg + wt[i];
        tatavg = tatavg + tat[i];
    }

    printf("\nPROCESS\t\tPRIORITY\tBURST TIME\tWAITING TIME\tTURNAROUND TIME");

    for (i = 0; i < n; i++)
        printf("\n%d \t\t %d \t\t %d \t\t %d \t\t %d ", p[i], pri[i], bt[i], wt[i], tat[i]);

    printf("\nAverage Waiting Time is: %f", wtavg / n);
    printf("\nAverage Turnaround Time is: %f", tatavg / n);

    getchar(); // To hold the console window
    return 0;
}





//prictical no 5


#include<stdio.h>
#include<conio.h>

int fr[3];

void display();

int main()
{
    int page[12] = {2, 3, 2, 11, 6, 2, 5, 5, 3, 2, 5, 2};
    int flag1 = 0, flag2 = 0, pf = 0, frsize = 3, top = 0, i, j;
    // clrscr();

    for(i = 0; i < 3; i++)
    {
        fr[i] = -1;
    }

    for(j = 0; j < 12; j++)
    {
        flag1 = 0; flag2 = 0;

        for(i = 0; i < frsize; i++)
        {
            if(fr[i] == page[j])
            {
                flag1 = 1; flag2 = 1; break;
            }
        }

        if(flag1 == 0)
        {
            for(i = 0; i < frsize; i++)
            {
                if(fr[i] == -1)
                {
                    fr[i] = page[j]; flag2 = 1; break;
                }
            }
        }

        if(flag2 == 0)
        {
            fr[top] = page[j];
            top++;
            pf++;
            if(top >= frsize)
                top = 0;
        }

        display();
    }

    printf("\nNumber of page faults: %d", pf + frsize);
    getch();
    return 0;
}

void display()
{
    int i;
    printf("\n");
    for(i = 0; i < 3; i++)
        printf("%d\t", fr[i]);
}





//experiment no 6

#include<stdio.h>
#include<conio.h>

void display();
int fr[3], n, m;

int main()
{
    int i, j, page[20], fs[10], max, found = 0, lg[3], index, k, l, flag1 = 0, flag2 = 0, pf = 0;
    float pr;

    printf("Enter length of the reference string: ");
    scanf("%d", &n);

    printf("Enter the reference string: ");
    for(i = 0; i < n; i++)
        scanf("%d", &page[i]);

    printf("Enter number of frames: ");
    scanf("%d", &m);

    for(i = 0; i < m; i++)
        fr[i] = -1;
    
    pf = m;

    for(j = 0; j < n; j++)
    {
        flag1 = 0;
        flag2 = 0;

        for(i = 0; i < m; i++)
        {
            if(fr[i] == page[j])
            {
                flag1 = 1;
                flag2 = 1;
                break;
            }
        }

        if(flag1 == 0)
        {
            for(i = 0; i < m; i++)
            {
                if(fr[i] == -1)
                {
                    fr[i] = page[j];
                    flag2 = 1;
                    break;
                }
            }
        }

        if(flag2 == 0)
        {
            for(i = 0; i < m; i++)
                lg[i] = 0;

            for(i = 0; i < m; i++)
            {
                for(k = j + 1; k < n; k++)
                {
                    if(fr[i] == page[k])
                    {
                        lg[i] = k - j;
                        break;
                    }
                }
            }

            found = 0;
            for(i = 0; i < m; i++)
            {
                if(lg[i] == 0)
                {
                    index = i;
                    found = 1;
                    break;
                }
            }

            if(found == 0)
            {
                max = lg[0];
                index = 0;
                for(i = 0; i < m; i++)
                {
                    if(max < lg[i])
                    {
                        max = lg[i];
                        index = i;
                    }
                }
            }
            fr[index] = page[j];
            pf++;
            display();
        }
    }

    printf("Number of page faults: %d\n", pf);
    pr = (float)pf / n * 100;
    printf("Page fault rate: %f\n", pr);

    getch();
    return 0;
}

void display()
{
    int i;
    for(i = 0; i < m; i++)
        printf("%d\t", fr[i]);
    printf("\n");
}
