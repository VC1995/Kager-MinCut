Kager-MinCut
============

Stanford's course on Algorithms : Design and Analysis, Part 1
Programming assignment 3
 (https://class.coursera.org/algo-006/quiz/start?quiz_id=52)

code in Java 
 
 
  import java.util.*;
  import java.io.*;
  public class U {
   ArrayList<Integer> vertices = new ArrayList<Integer>();
   ArrayList<Integer> adjacent = new ArrayList<Integer>();
   public void addVertex(int a) {
        vertices.add(a);
    }
    
   public void addAdjacent(int a ) {
        adjacent.add(a) ;
    }
    
   public String toString(){
        String result="Vertices = "+vertices.toString()+"\n Adjacent vertices = "+adjacent.toString();
        return result;
    }
    
   public void addU(U a){
        vertices.addAll(a.getVertices());
        adjacent.addAll(a.getAdjacent());
        ArrayList<Integer> toBeRemoved=new ArrayList<Integer>();
        int j=0;
        for(int i=0;i<adjacent.size();i++) {
            if( vertices.contains ( adjacent.get(i) ) ) {
                toBeRemoved.add( adjacent.get(i) );
                j++;
            }
        }
        for(int i=0;i<j;i++) {
            while( adjacent.indexOf(toBeRemoved.get(i)) != -1 ) {
                adjacent.remove( adjacent.indexOf(toBeRemoved.get(i)) ) ;
            }
        }
        
    }
    
   public ArrayList<Integer> getAdjacent(){
        return adjacent;
    }
    
    public ArrayList<Integer> getVertices(){
        return vertices;
    }
    
    public String showVertices(){
        return vertices.toString();
    }
}
    

  public class MinCut
  {   ArrayList<U> V=new ArrayList<U>();
    public static void main(String[] Args){
        MinCut problem1 = new MinCut();
        problem1.go();
  }

public void go() {
    loadVertices();
    int min=10000;    
    for(int i=0;i>-1;i++) {
        V.clear();
        loadVertices();
        
        while(V.size()>2) {
            int first = (int) ( Math.random() * V.size() ) ;
            U a=V.get(first) ;
            
            int forSecond =  (int) ( Math.random() * a.getAdjacent().size() ) ;
            
            int secondMustBe=a.getAdjacent().get(forSecond);
            U b=new U();
            for( int k=0;k<V.size();k++ ) {
                b=V.get(k);
                if( b.getVertices().contains(secondMustBe) ) break;
            }
                                  
            a.addU(b);
            
            V.remove(b);
            
        }
        System.out.println(i);
        //System.out.println( V.get(0) + " and size = "+V.get(0).getAdjacent().size() + "\n " + V.get(1) + " and size = "+V.get(1).getAdjacent().size());
        min = Math.min( min , V.get(0).getAdjacent().size() );
        
    }
    
    System.out.println("Min. = " +min);

}

public void loadVertices() {
    try {
        FileReader fileReader=new FileReader(new File("MinCut.txt"));
        BufferedReader reader= new BufferedReader(fileReader);
        String result=null;
        while((result=reader.readLine())!=null) {
           
            String[] numbers=result.split("\t");
            U thisOne=new U();
            thisOne.addVertex ( Integer.parseInt(numbers[0]) );
            for(int i=1;i<numbers.length;i++) {
                thisOne.addAdjacent( Integer.parseInt(numbers[i]) ) ;
            }
            V.add(thisOne) ;
            //System.out.println(thisOne);
        }
        reader.close();
    }
    catch(IOException e) {}
    
}

}
