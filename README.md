<div align="center">

## samples of seven sort algorithms


</div>

### Description

Clear examples of: insertion, selection, shellsort, quicksort, mergesort, badsort

Please let me know if anything wrong with it

and please rate it.
 
### More Info
 
input is hardwired, but you can change global variable SIZE in order to change v.size().

Example can execute only one algorithm at a time,

to see different one simply uncomment one that you would like to experiment with

returns initial and sorted vector

badsort can cause system to freeze,    so set SIZE >= 5


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Erik Minkin](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/erik-minkin.md)
**Level**          |Beginner
**User Rating**    |3.6 (18 globes from 5 users)
**Compatibility**  |C\+\+ \(general\)
**Category**       |[Sorting](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/sorting__3-24.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/erik-minkin-samples-of-seven-sort-algorithms__3-3279/archive/master.zip)





### Source Code

```
#include <iostream>
#include <iomanip>
#include <cstdlib>
#include <ctime>
using namespace std; //introduces namespace std
const int SIZE = 20;
void fill_vector(vector<int> & v);
ostream & operator<<(ostream & out , const vector<int> & v);
void selection(vector<int> & v);
void insertion(vector<int> & v);
void shellsort( vector<int> & v );
void quicksort( vector<int> & v, int low, int high);
void mergesort( vector<int> & v, int low, int high);
void merge( vector<int> & v, int low, int middle, int high);
void badsort( vector<int> & v);
bool sorted(const vector<int> & v);
//void swap( int & a,int & b);
int main ( void )
{
 vector <int> v;
 fill_vector(v);
	cout << v << endl << "This is a test of sort\n";
	//insertion (v);
	//selection (v);
	//sort(v.begin(), v.end()); // STL
	//shellsort(v);
	quicksort(v , 0, v.size()-1);
	// mergesort(v, 0, v.size() - 1);
	//badsort(v);
	cout << v << endl;
	return 0;
}
void fill_vector(vector<int> & v)
{ srand(time(0));
 for (int i = 0; i < SIZE;i++)
  v.push_back(rand() % 1000);
}
/* already in STL
void swap( int & a,int & b)
{int tem = a;
  a = b;
  b = tem;
 }
*/
void selection(vector<int> & v)
{
 int low;
 for (int i = 0; i < v.size() - 1; i++)
 {
 low = i;
 for (int j = i+1; j <v.size(); j++)
  if (v[low] > v[j])
  low = j;
 if ( low != i)
  swap (v[i] , v[low]);
 }
}
void insertion(vector<int> & v)
{int j;
 for (int i = 1; i < v.size(); i++)
 {
 int tem = v[i];
 for ( j = i ; j > 0 && v[j - 1] > tem; j--)
 v[j] = v[j-1];
 if (j != i)
 v[j] = tem;
 }
 }
void shellsort( vector<int> & v )
{
 int j;
 for( int gap = v.size( ) / 2; gap > 0;
    gap = gap == 2 ? 1 : gap / 2.2 )
  for( int i = gap; i < v.size( ); i++ )
  {
   int tmp = v[ i ];
   for( j = i; j >= gap && tmp < v[ j - gap ]; j -= gap )
    v[ j ] = v[ j - gap ];
   v[ j ] = tmp;
  }
}
void quicksort( vector<int> & v, int low, int high)
{
 if ( low < high)
 { // choose pivot as median of v[low],v[middle],v[high]
 int i , j;
 int middle = (low + high) / 2;
 cout << "initially low and high " << low << " " << high << endl;
 for (i=low; i <= high; i++)
  cout << v[i] << " ";
 if(v[low] > v[middle])
  swap (v[low] ,v[middle]);
 if (v[low] > v[high])
  swap(v[low] , v[high]);
 if (v[middle] > v[high])
  swap( v[middle], v[high]);
 int pivot = v[middle];
 swap (v[middle] , v[high-1]);
 //partition
 cout << "\nafter picking pivot = " << pivot << endl;
 for (i=low; i <= high; i++)
  cout << v[i] << " ";
 if (high -low > 2
 )
 {
  for (i = low , j = high -1; ;)
  {
  while (v[++i] < pivot );
  while (j > 0 && v[--j] > pivot);
  if ( i < j)
   swap (v[i], v[j]);
  else
   break;
  }
  swap(v[i], v[high-1]);
  cout << "\nafter partition " << endl;
  for (int k=low; k <= high; k++)
  cout << v[k] << " ";
 quicksort(v , low, i-1);
 quicksort(v , i+1, high);
 }
 }
}
void mergesort( vector<int> & v, int low, int high)
{
 if (low < high)
 {
 int middle = (low + high) / 2;
 mergesort(v, low,middle);
 mergesort(v, middle+1,high);
 merge( v , low , middle,high);
 }
 }
void merge( vector<int> & v, int low, int middle, int high)
{
 cout << "merge with low = " << low << " and high = " << high << endl;
 for (int i=low; i<=high;i++)
 cout << v[i] << " ";
 vector<int> tem(high-low+1);
 int lowin = low, highin = middle + 1, temin = 0;
 while (lowin <= middle && highin <= high)
 {
 if (v[lowin] < v[highin])
  tem[temin++] = v[lowin++];
 else
  tem[temin++] = v[highin++];
 }
 while (lowin <= middle)
 {
  tem[temin++] = v[lowin++];
 }
 while ( highin <= high)
 {
  tem[temin++] = v[highin++];
 }
 for (int i=0; i < high-low+1; i++)
 v[low+i] = tem[i];
 for (int i=low; i<=high;i++)
 cout << v[i] << " ";
 cin.get();
 }
void badsort( vector<int> & v)
{
 while (!sorted(v))
 next_permutation(v.begin(), v.end());
// random_shuffle(v.begin(),v.end());
}
bool sorted(const vector<int> & v)
{static int counter = 0;
 cout << "counter = " << counter++ << endl;
 bool ok = true;
 for (int i=1; ok && i<v.size(); i++)
 if ( v[i-1] > v[i])
 ok = false;
 return ok;
}
ostream & operator<<(ostream & out , const vector<int> & v)
{
 for (int i=0 ; i< v.size(); i++)
 out << (i%5? ' ' : '\n') << setw(8) << v[i] ;
 return out;
}
```

