/*

https://leetcode.com/problems/range-sum-query-2d-immutable/description/

Given a 2D matrix matrix, handle multiple queries of the following type:

Calculate the sum of the elements of matrix inside the rectangle defined by its upper left corner (row1, col1) and lower right corner (row2, col2).
Implement the NumMatrix class:

NumMatrix(int[][] matrix) Initializes the object with the integer matrix matrix.
int sumRegion(int row1, int col1, int row2, int col2) Returns the sum of the elements of matrix inside the rectangle defined by its upper left corner (row1, col1) and lower right corner (row2, col2).
You must design an algorithm where sumRegion works on O(1) time complexity.




To handle region sum queries in O(1) time, you need to pre-calculate the sums of all possible rectangles that start from the origin (0, 0). By storing these values, you can find the sum of any arbitrary rectangle using a simple arithmetic formula.

This technique is often called a summed-area table or prefix sum matrix.

The Core Idea 💡
The strategy is to create a new matrix, let's call it sumMatrix, where sumMatrix[r][c] stores the sum of all elements in the rectangle from (0, 0) to (r-1, c-1) of the original matrix.

Once this sumMatrix is built, the sum of any rectangle can be calculated in constant time using the principle of inclusion-exclusion.

As the diagram shows, the sum of the desired green rectangle can be found by:

Taking the sum of the large rectangle (D).

Subtracting the sums of the two overlapping rectangles (B and C).

Adding back the sum of the small corner rectangle (A), because it was subtracted twice.

Sum(Green) = Sum(D) - Sum(B) - Sum(C) + Sum(A)

This calculation only requires four lookups in our pre-computed sumMatrix, making it an O(1) operation.

 1. The Constructor: NumMatrix(int[][] matrix)
The constructor's job is to build the sumMatrix. It iterates through the input matrix and calculates the value for each cell using the following formula:

sumMatrix[r][c] = matrix[r-1][c-1] + sumAbove + sumToLeft - sumOfOverlap


*/




class NumMatrix {

    // This matrix will store the pre-calculated sums.
    private int[][] sumMatrix;

    /**
     * Constructor: Initializes the data structure by pre-calculating sums.
     * Time Complexity: O(m * n) where m is rows, n is cols.
     * Space Complexity: O(m * n)
     */
    public NumMatrix(int[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return;
        }

        int rows = matrix.length;
        int cols = matrix[0].length;

        // Initialize sumMatrix with an extra row and column to simplify formulas.
        sumMatrix = new int[rows + 1][cols + 1];

        // Build the summed-area table.
        for (int r = 1; r <= rows; r++) {
            for (int c = 1; c <= cols; c++) {
                // Formula: current value + sum above + sum to the left - overlapping corner

                /*
                The current value is matrix[r - 1][c - 1] instead of matrix[r][c] because the sumMatrix we build is one size larger than the original matrix. We add an extra row and column of zeros as padding.
                */
                
                sumMatrix[r][c] = matrix[r - 1][c - 1] 
                                + sumMatrix[r - 1][c] 
                                + sumMatrix[r][c - 1] 
                                - sumMatrix[r - 1][c - 1];
            }
        }
    }

    /**
     * Calculates the sum of the specified rectangular region in O(1) time.
     * Time Complexity: O(1)
     */
    public int sumRegion(int row1, int col1, int row2, int col2) {
        // Using the inclusion-exclusion principle with our pre-calculated matrix.
        // We add 1 to the indices because our sumMatrix is padded.
        int totalSum = sumMatrix[row2 + 1][col2 + 1]; // D
        int topSum = sumMatrix[row1][col2 + 1];       // B
        int leftSum = sumMatrix[row2 + 1][col1];      // C
        int topLeftSum = sumMatrix[row1][col1];       // A

        return totalSum - topSum - leftSum + topLeftSum;
    }
}
