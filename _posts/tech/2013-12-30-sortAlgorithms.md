---
layout: post
title: sortAlgorithms
category: 技术
tags: sort Algorithms
keywords: sort Algorithms
description:
---

```
#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;


//数的交换
void swap( int* _va, int* _vb )
{
     if( *_va==*_vb )
     {
          return;
     }
     *_va = *_va + *_vb;
     *_vb = *_va - *_vb;
     *_va = *_va - *_vb;
}

//寻找数组最大值
int findMax( int *arr, int len )
{
     int max = arr[0];
     for( int i = 1; i != len; ++i )
     {
          if( arr[i]>max)
          {
               max = arr[i];
          }
     }
     return max;
}
//寻找第二大数
int findSecondMax( int *arr, int len )
{
     int max = arr[0];
     int smax = arr[1];
     for( int i = 1; i != len; ++i )
     {
          if( arr[i]>max)
          {
               smax = max;
               max = arr[i];
          }else if( arr[i] > smax )
          {
               smax = arr[i];
          }
     }
     return smax;
}
//逆置数组
void arrayReverse( int* arr, int len )
{
     int i = 0, j= len-1;
     while( i < j )
     {
          swap( arr+i, arr+j );
          ++i;
          --j;
     }
}
//循环右移k位
//方法一
void rightShift( int* arr, int len, int k )
{
     for(int i = 0; i != k; ++i )
     {
          int tmp = arr[ len -1 ];
          for( int j = len-1; j != 0; --j )
          {
               arr[j] = arr[j-1];
          }
          arr[0] = tmp;
     }
}
//方法二
void rightShift2( int* arr, int len, int k )
{
     arrayReverse( arr, k);
     arrayReverse( arr, len-k);
     arrayReverse( arr, len );
}

//冒泡排序
void bubbleSortZc( int* arr, int len )
{
     for (int i = 0;i<len;++i)
     {
          int change = 1;
          for (int j = 0;j<len - i-1;++j)
          {
               if (arr[j]>arr[j+1])
               {
                    swap(arr+j,arr+j+1);
                    change = 0;
               }
          }
          if (change) break;
     }
}
void bubbleSort( int* arr, int len )
{
     for( int i = 0; i != len-1; ++i )
     {
          for( int j = i+1; j != len; ++j )
          {
               if( arr[j] < arr[i] )
               {
                    swap( arr+i, arr+j );
               }
          }
     }
}

//选择排序
void selectSort( int* arr, int len )
{
     for( int i = 0; i != len; ++i )
     {
          int sIndex = i;
          for( int j = i+1; j != len; ++j )
          {
               if( arr[j] < arr[sIndex] )
               {
                    sIndex = j;
               }
          }
          if( sIndex != i )
          {
               //交换
               swap( arr+sIndex, arr+i );
          }
     }
}
//插入排序
void insertSort( int* arr, int len )
{
     for( int i = 1; i != len; ++i )
     {
          int tmp = arr[ i ];
          //线性右移腾出插入位置
          int j = i-1;
          for( ; arr[j]>tmp; --j )
          {
               arr[j+1] = arr[j];
          }
          arr[j+1] = tmp;
     }
}


//快速排序
int partition(int *A,int left,int right)
{
     int pivot = A[left];
     while (left<right)
     {
          while (left<right && A[right]>=pivot) right--;
          A[left] = A[right];
          while (left<right && A[left]<=pivot) left++;
          A[right] = A[left];         
     }
     A[left] = pivot;
     return left;
}

void quickSort2(int *A,int left,int right)
{
     if (left<right)
     {
          int mid = partition(A,left,right);
          quickSort2(A,left,mid-1);
          quickSort2(A,mid+1,right);
     }
    
}


void quikSort( int* arr, int left, int right )
{
     int mid = (left+ right)/2;
     int _lpos = left;
     int _rpos = right;
     do {
          while( arr[ _lpos ] < arr[mid] ) ++_lpos;
          while( arr[ _rpos ] > arr[mid] )  --_rpos;
          if( _lpos <= _rpos )
          {
               swap( arr+_lpos, arr+_rpos );
               ++_lpos;
               --_rpos;
          }
     }while( _lpos <= _rpos );
     if( left < _rpos )
     {
          quikSort( arr, left, _rpos );
     }
     if( right > _lpos )
     {
          quikSort( arr, _lpos, right );
     }
}

//大顶堆向下调整操作
void heapSiftdown( int* arr, int len , int pos )
{
     if( 2*pos+1 >= len )
     {
          return;
     }
     bool flag = false;
     while( 2*pos+1<len && !flag )
     {
          //要调整位置的左子结点，这时候要调整的位置变成(pos-1)/2
          pos = pos*2+1;
          //与左右子节点较大者交换
          if( pos+1 < len && arr[ pos ]<arr[ pos+1 ] )
          {
               ++pos;
          }
          if( arr[ (pos-1)/2 ] < arr[ pos ] )
          {
               swap( arr+(pos-1)/2, arr+pos);
          }else{
               flag = true;//左右子节点都比本结点小，调整结束
          }
     }
}
//堆排序
void heapSort( int* arr, int len )
{
     //建堆
     for( int i = len/2-1; i>=0; --i )
     {
          heapSiftdown( arr, len, i );
     }
     //排序
     for( int i = len-1; i != 0; --i )
     {
          swap( arr, arr+i );
          heapSiftdown( arr, i, 0);
     }
}

//打印数组
void printArray( int* arr, int len )
{
     for( int i = 0; i != len-1; ++i )
     {
          cout<<arr[i]<<" ";
     }
     cout<<arr[ len-1 ]<<endl;
}

//随机打乱数组，用于测试
void my_shuffer( int* arr, int len )
{
     for( int i = 0; i != len; ++i )
     {
          int j = i + rand()%(len-i);
          if( i!=j )
          {
               swap( arr+i, arr+j );
          }

     }
}

int main( )
{
     int data[1024];
     int len;
     while( cin>>len&&len!=0 )
     {
          for( int i = 0; i != len; ++i )
          {
               cin>>data[i];
          }
          cout<<"Max:"<<findMax( data, len )<<endl;
          cout<<"Second Max:"<<findSecondMax( data, len )<<endl;
          //逆置数组
         arrayReverse( data, len );
          cout<<"Reverse the Array:";
          printArray( data, len );
          //循环右移0到len位
          for( int i = 0; i <= len; ++i )
          {
               rightShift( data, len, i);
               cout<<"Right Shift "<<i<<" position(s):";
               printArray( data, len );
          }
          //循环右移0到len位
          for( int i = 0; i <= len; ++i )
          {
               rightShift2( data, len, i);
               cout<<"Right Shift "<<i<<" position(s):";
               printArray( data, len );
          }
          //冒泡排序
          bubbleSort( data, len );
          cout<<"After select sort:";
          printArray( data, len );

          //随机化数组
         srand( unsigned( time(NULL) ) );
          my_shuffer( data, len );
          cout<<"Shuffer the Array:";
          printArray( data, len );

          //插入排序
          insertSort( data, len );
          cout<<"After select sort:";
          printArray( data, len );

          //随机化数组
         my_shuffer( data, len );
          cout<<"Shuffer the Array:";
          printArray( data, len );

          //选择排序
          selectSort( data, len );
          cout<<"After select sort:";
          printArray( data, len );

          //随机化数组
         my_shuffer( data, len );
          cout<<"Shuffer the Array:";
          printArray( data, len );
          //快排
          quikSort( data, 0, len-1 );
          cout<<"After quick sort:";
          printArray( data, len );
         
          //随机化数组
         my_shuffer( data, len );
          cout<<"Shuffer the Array:";
          printArray( data, len );
         
          //堆排序
          heapSort( data, len );
          cout<<"After heap sort:";
          printArray( data, len );
     }
     return 0;
}
```



