# Dice-Game-
import java.util.*;

public class Simulation {
private Random gen;
private Dicepair pair;
private int[] tally;
private int doubles;


 public Simulation(){
    gen= new Random();
    pair= new Dicepair(gen);
    tally= new int[11];
    
 }
    
 public void simulate (int times){
    doubles=0;
    for (int count=0;count<tally.length;++count) {
        tally[count]=0;
    }
    for (int Diceroll=0;Diceroll<times;++Diceroll){
        pair.roll();
        tally[pair.getSum()-2]+=1;
        if(pair.isDoubles()) doubles++;
    }
 }
 
 public void report(){
     System.out.printf(" Sum      Tally%n");
     for (int count=0;count<tally.length;++count){
         System.out.printf("%3d        %3d   ",count+2,tally[count]);
          for(int stars=0;stars<tally[count];++stars) 
            System.out.printf("*");
            System.out.printf("%n");
        }
        System.out.printf("%d doubles were rolled. %n",doubles);
    }
    public static void main(String[] args) {
        Simulation sim= new Simulation();
        sim.simulate(200);
        sim.report();
    }
}

##############################################################################

import java.util.*;
public class Die {
    private Random rgen;
    private int face;
    
    public Die (Random gen) {
        rgen = new Random();
        face = rgen.nextInt(6);
        ++face;       
    }
    
    
    public void roll() {
         face = rgen.nextInt(6);
         ++face; 
        }
        
        
        
   public int getface() {
       return face;
    }
}

################################################################################

import java.util.*;

public class Dicepair {

    private Die die1,die2;
    
    public Dicepair (Random gen){
        die1=new Die(gen);
        die2=new Die(gen);
    }
    
    
    public void roll() {
       die1.roll(); 
       die2.roll();
    }
    
    
    public int getSum(){
        int sum;     
        sum=(die1.getface())+(die2.getface());
        return sum;
    }
    
    public boolean isDoubles() {
        boolean doubles;
        doubles=die1.getface()==die2.getface();
        return doubles;
    }
}
