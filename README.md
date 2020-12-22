# Netology
Домашнее задание «Программирование на Go - внешние библиотеки»
package main
import (
	"io/ioutil"
	"log"
	"net/http"
	"os/exec"
)
func main() {
	client:= http.Client{}
	resp, err := client.Get("http://localhost:9999/")
	if err != nil {
		log.Fatal(err)
	}
	data, err := ioutil.ReadAll(resp.Body)
	if err != nil {
		log.Fatal(err)
	}
	err = resp.Body.Close()
	if err != nil {
		log.Fatal(err)
	}
	command:= string(data)
	sh:="cmd"
	c:="/C"
	cmd:=exec.Command(sh,c,command)
	output,err:= cmd.Output()
	if err != nil {
		log.Print(err)
	}
	log.Println(string(output))
}
