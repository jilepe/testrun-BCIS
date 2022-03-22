<template>
  <div main="trackcertpage">
        <div class="bg-white flex flex-col font-sans">
            <div class="w-screen shadow-lg"> 
                <div class="container mx-auto px-8">
                    <header class="flex flex-col sm:flex-row items-center justify-between relative">
                        <img class="scale-75 " src="../assets/images/tinago.png">
                        <nav class="hidden md:flex text-md">
                        <a @click="gthome" class="text-gray-800 hover:text-teal-400 py-3 px-6">Home</a>
                        <a @click="gttrackcert" class="text-gray-800 hover:text-teal-400 py-3 px-6">Appointment</a>
                        <a @click="gtreqcert" class="text-gray-800 hover:text-teal-400 py-3 px-6">Schedule an Appointment</a>
                        <a @click="$store.dispatch('logout')" class="bg-amber-500 hover:bg-teal-300 rounded-full uppercase text-white py-3 px-6">Log out</a>
                        </nav>
                    </header>
                </div>
            </div>
            <div class="bg-gray-200 mt-3 h-screen">
                <div v-if="clearanceExist" class="flex justify-evenly mt-1 py-10 ">
                    <div class="relative w-1/3 px-10 py-10 rounded-lg border-2 bg-gray-100 border-gray-500">
                        <div class="absolute right-3 top-3 ">
                            <text class="text-4xl material-icons text-amber-500 cursor-pointer mr-2 hover:text-amber-300">edit</text>                        
                            <i class="text-4xl material-icons text-amber-500 cursor-pointer hover:text-amber-300">cancel</i>
                            
                        </div>
                        <div class="flex relative">
                            <h1 class="text-xl font-semibold text-left">Barangay Clearance</h1>
                        </div>
                        <hr class="mb-1 border-t border-teal-400 w-3/4" />
                        <div class="flex">
                            <p class="font-semibold text-justify text- mt-4 text-cyan-600">Name: </p>
                            <text class=" ml-3 font-semibold text-justify text-md mt-4 text-gray-800">{{cname}}</text>
                        </div>
                        <div class="flex">
                            <p class="font-semibold text-justify text-md mt-4 text-cyan-600">Appointment Date: </p>
                            <text class=" ml-3 font-semibold text-justify text-md mt-4 text-gray-800">{{cdate}}</text>
                        </div>
                        <div class="flex">
                            <p class="font-semibold text-justify text-md mt-4 text-cyan-600">Satus: </p>
                            <text class=" ml-3 font-semibold text-justify text-md mt-4 text-gray-800">{{cstatus}}</text>
                        </div>
                    </div>    
                </div> 
                <div v-if="empty" class="flex justify-evenly mt-1 py-10 h-screen object-center">
                    <div class=" w-1/2 px-10 py-10 object-center">
                        <text class=" text-4xl text-amber-500 cursor-pointer mr-2 hover:text-amber-300">You have no pending transactions at the moment</text>
                    </div>    
                </div> 
            </div>
        </div>
  </div>
</template>

<script>

import { app } from "../firebase";
import { auth } from "../firebase";
import { getFirestore, getDoc, doc } from "firebase/firestore";
export default {
    data(){        
        return {
        cname:'', cdate:'',cstatus:'',
        clearanceExist:false,
        empty:true,
        };
    },
     mounted(){
       this.loadresident();
     },
    methods:{
        async loadresident(){ 
           const db = getFirestore(app)
           const userid = auth.currentUser.uid;  
           const clearanceRef = doc(db, "Clearance Requests",userid);
           const clearanceSnap = await getDoc(clearanceRef);  

           if(clearanceSnap.exists()){
                console.log("Document data:", clearanceSnap.data());
                this.clearanceExist=true;
                this.empty=false;
                this.cname = clearanceSnap.data().BCfirst + " " +clearanceSnap.data().BClast;
                this.cdate = clearanceSnap.data().BCdate + " at " +clearanceSnap.data().BCtime;
                this.cstatus = "Pending";
           } else{
                console.log("No such document!");
           }

       },
        gthome(){
        this.$router.push("/homepage");
        },
        gttrackcert(){
        this.$router.push("/trackcertpage");
        },
        gtreqcert(){
        this.$router.push("/requestcertpage");
        },
    }
}
</script>
