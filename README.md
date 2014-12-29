Scala-Codes-
cypher encryption 
============

import scala.io.Source
import scala.util.Random
import java.io.PrintWriter

main()


def main() {
if(args(0)=="encrypt") 	
	encryptMode(args(1),args(2))
//args(0)is encrypt
//args(1)the plain text filename to be encrypted (the input file)


//args(2)the output filename stub

else if(args(0)=="decrypt")
     decryptMode(args(1),args(2))

else {
	println("Error, please try 'encrypt' or 'decrypt'.")
	println("Exit program.")
	}
}

def encryptMode(readFrom:String, writeTo:String) {
val key  = new PrintWriter(writeTo+".key")
val msg = new PrintWriter(writeTo+".msg")
val input = Source.fromFile(readFrom)
    for (c <- input) {
	if(c>=' ' && c<='~'){
	var keychar = (Random.nextInt(95)+32).toChar
	key.print(keychar)
	msg.print((((c-' ')+(keychar-' '))%'^'+' ').toChar)
			}
		else { 
			key.print(c)
			msg.print(c)
			}
		}
	input.close
	key.close
	msg.close
}

def decryptMode(readFrom:String, writeTo:String){
val key = Source.fromFile(readFrom+".key")
val msg = Source.fromFile(readFrom+".msg")
val output = new PrintWriter(writeTo)
for(c <-msg) {
	if(c>=' ' && c<='~'){
	output.print(((c-' '+'^'-key.next+' ')%'^'+' ').toChar)
			}	
		else { 
			key.next
			output.print(c)	
			}
		}
	key.close
	msg.close
	output.close
}



