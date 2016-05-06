##MATLAB CHEAT SHEET
###For developers who need to convert MATLAB code into "normal" code.


#### Length
*Returns the number of rows in a matrix or vector*

######MATLAB example

```
n = length(matrixA);
```
___


#### Row Sums
*Returns a vector containing the sums of each row*

######MATLAB example

```
Rowsum_Vector = sum(A,2);  
// note that 2 denotes the dimension in which the values are returned
//  essentially the vector returned would be an additional column 
//  containing the sum of values in each row

matrixA = [1,2,3;4,5,6;7,8,9]

Rowsum_vector = sum(matrixA,2) = [12,15,18]
```
___


#### Column Sums
*Returns a vector containing the sums of each column*

######MATLAB example

```
ColumnSum_vector = sum(matrixA,1);
```
___


#### Matrix Transposition
*Returns a transposed matrix*

######MATLAB example

```
TransposedMatrix = (A)’;
```

This is often used in conjunction with other methods:

```
TransposedMatrix = sum(A,2)’;
```
___


#### Vector Division
*Returns a vector in which each value has been divided by a constant*

######Matlab Example

```
VectorB = VectorA/ConstantA
```

ConstantA will generally be an average, sum of sums, or some other previously calculated value.
___


####Loop Iteration
*Loop iteration is expressed as (startingValue, incrementByValue, endValue) where endValue is generally expressed as a function of the length of the vector being iterated*

######MATLAB example
```
for y = 1:1:n
	for x1 = 1:1:n
```

######C# equivalent
```
for (int row = 0; row < rowCount; row++)
            { 
		for (int col = 0; col < columnCount; col++)
               	 {  // logic }
	}
```
	
######Another MATLAB example
```
for u2= 1:1:n-1
    for v2= u2+1:1:n
```

######C# equivalent
```
for(var row = 0; i< rowCount -1; row++) 
	{ 
		for(var col = row + 1; row < rowCount; row++ )
		{ // logic }			
	}
```
___


####Matrix copy

*Copy values > 0 from one matrix to another (values < 0 become 0)*

######MATLAB example
```
for y = 1:1:n
   for x = 1:1:n
       if matrixA(x,y)>0
          matrixB(x,y)= matrixA(x,y);
        else
          matrixB(x,y)=0;
        end
    end
```
___


####Data Validation
*Check for NaN or infinite values, change to 0*

######MATLAB example
```
F(isnan(F)) = 0;
F(isinf(F)) = 0;
```

######C# equivalent
```
for(var row = 0; i< rowCount -1; row++) 
	{ 
		for(var col = row + 1; row < rowCount; row++ )
		{ 
			if(matrix[row,col] <= 0 || double.IsNaN(matrix[row,col])
				{ matrix[row,col] = 0; }
		}			
	}
```
___


###Logarithm
*Calculate the natural logarithm of each value in a matrix*

######MATLAB example
```
matrix = log(matrixA);
```

######C# equivalent
```
for(var row = 0; i< rowCount -1; row++) 
	{ 
		for(var col = row + 1; row < rowCount; row++ )
		{ 
			matrixB[row, col] = Math.Log(matrixA[row, col], 2);
		}			
	}
```
___

####Indexing
*Explanation of shorthand notations for extracting column and rows as vectors*

**MATLAB example**
```
// extract row ‘n’ as a vector
rowVector = matrix(n,:);
// extract the last column as a vector
columnVector = matrix(:,end);
```
___


####Hadamard products (aka element-wise multiplication)
*Returns a matrix where each value xy is the product of elements xy in the two original matrices.
The Matlab notation for Hadamard products is often confused with the notation for a scalar product (aka, dot product).  Don’t make this mistake.*

######MATLAB example
```
matrixC = matrixA.*matrixB;
```

######C# equivalent
```
for(var row = 0; i< rowCount -1; row++) 
	{ 
		for(var col = row + 1; row < rowCount; row++ )
		{ 
			matrixC[row, col] = matrixA[row,col] * matrixB[row,col];
		}			
	}
```
___


####Scalar product (aka dot product) of vectors
*Returns the scalar product of two vectors*

######MATLAB example
```
vectorC = dot(vectorA,vectorB);
```

######C# equivalent
```
int result = 0;
for(int i = 0; i<vectorLength;i++)
	{	result += vectorA[i]*vectorB[i]; }
return result;
```
___


####Scalar product (aka dot product) of matrices 
*Returns a vector of scalar products where each column is treated as a vector, and the result is the scalar product of each column*

######MATLAB example
```
vectorC = dot(matrixA, matrixB); 
```

How this works is the columns of each matrix are turned into vectors, then a standard scalar product is calculated between each corresponding value.

So, this:
```
vectorC = dot(matrixA, matrixB); 
```

is broken down into this:
```
vectorC[i] = dot(matrixA(:,i),matrixB(:,i);
```
 
To calculate a vector of the scalar product of two matrices where rows are treated as vectors, the MATLAB method is overloaded with a value for the dimension

######MATLAB example
```
vectorC = dot(matrixA, matrixB, 2);
```

which is broken down into this:
```
vectorC[i] = dot(matrixA(i,:),matrixB(i,:);
```
