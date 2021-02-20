# hackerrank_cristian
Solutions of hackerrank

**Day 10: Binary Numbers**
int n = scanner.nextInt();
scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");
int counter = 0, max =0;
while (n > 0) {
    int rem = n%2;
    if (rem==1) counter++; 
    else counter=0;
    max = Math.max(counter, max);
    n/=2;
}
System.out.println(max);

