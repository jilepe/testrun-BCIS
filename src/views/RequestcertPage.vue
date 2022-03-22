<template>
    <div main="requestcertpage">
        <div class="bg-white flex flex-col font-sans">
            <div class="w-screen shadow-md"> 
                <div class="container mx-auto px-8">
                    <header class="flex flex-col sm:flex-row items-center justify-between relative">
                        <img class="scale-75 " src="../assets/images/tinago.png">
                        <nav class="hidden md:flex text-md">
                        <a @click="gthome" class="text-gray-800 hover:text-teal-400 py-3 px-6">Home</a>
                        <a @click="gttrackcert" class="text-gray-800 hover:text-teal-400 py-3 px-6">Appointment</a>
                        <a @click="gtreqcert" class="text-gray-800 hover:text-teal-400 py-3 px-6">Schedule an Appointment</a>
                        <a @click="$store.dispatch('logout')" class=" right-1 bg-amber-500 hover:bg-teal-300 rounded-full uppercase text-white py-3 px-6">Log out</a>
                        </nav>
                    </header>
                </div>
            </div>
            
            <div class="flex">                        
                <div class="w-1/4 mt-5 px-10 text-left">
                    <ion-label class="font-bold text-amber-500 uppercase">Request Certificate</ion-label>  
                    <div class="block mt-10  w-60">
                        <ul class="whitespace-nowrap">
                        <li v-if="dat1" @click="DateTime" class="bg-none hover:bg-teal-100 border border-gray-400 text-gray-500 px-1"> Date and Time</li>
                        <li v-if="dat2" class="bg-none hover:bg-teal-100 border border-gray-400 text-amber-500 px-1"> Date and Time</li>
                        <li v-if="ai1" @click="AppInfo" class="bg-none hover:bg-teal-100 border border-gray-400 text-gray-500 px-1"> Application Information</li>
                        <li v-if="ai2" class="bg-none hover:bg-teal-100 border border-gray-400 text-amber-500 px-1"> Application Information</li>
                        <li v-if="rai1" class="bg-none hover:bg-teal-100 border border-gray-400 text-gray-500 px-1"> Review Application Information</li>
                        <li v-if="rai2" class="bg-none hover:bg-teal-100 border border-gray-400 text-amber-500 px-1"> Review Application Information</li>
                        </ul>
                    </div>                   
                </div>  
                <div class="w-3/4 h-screen">  
                    
                    <div v-if="start" class="w-3/4 mt-5">
                        <form class="">
                        <h1 class="text-2xl font-semibold text-left">Notes and Instructions: </h1>
                            <p class="font-semibold text-justify text-lg mt-4 text-cyan-600">Valid Resident ID</p>
                            <p class="font-normal text-justify ml-6">
                                Upon claiming the requested certificate, the resident must bring atleast 1 valid ID with
                                him/her to claim the certificate that he/she requested.
                            </p>
                            <p class="font-semibold text-justify text-lg mt-4 text-cyan-600">Resident Cedula</p>
                            <p class="font-normal text-justify ml-6">
                                Cedula is also a requirement for the resident to claim the certificate he/she requested.
                                The resident can bring his/her cedula if he/she has a valid cedula, if the resident doesnt have a cedula
                                it will be included in the request.
                            </p>

                            <div class="w-full flex justify-evenly mt-10">
                            <div @click="DateTime" class="w-1/4 h-10 rounded-full bg-amber-500 hover:bg-amber-300 mt-3 text-center cursor-pointer text-xl text-white font-medium py-1">Proceed</div>   
                            </div>        
                        </form>  
                    </div>            
                    <div v-if ="OptionDateTime" >
                        <div class="flex justify-around mt-5 px-5">
                            <div class="">
                                <ion-label class="font-bold text-amber-500 uppercase">Date</ion-label>
                            </div>
                            <div class="">
                                <ion-label class="font-bold text-amber-500 uppercase">Time</ion-label>
                            </div>
                        </div>
                    </div>
                    <div v-if ="OptionAppInfo" class="w-full"> 
                        <div class=" h-screen">
                            <div class="mt-5 mb-4 text-left">
                                <label class="font-bold text-amber-500 uppercase">Application Information</label>
                            </div>
                            <div class="flex px-5">
                                <div class="w-full flex">
                                        <label class="block mt-2 text-lg font-semibold text-gray-600 mx-3">Certificate Type:</label>
                                        <select v-model="ctype"
                                        class="py-2 px-3 rounded-lg border-2 font-semibold border-teal-400 mt-1 focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent">
                                            <option value= "BARANGAY CLEARANCE">BARANGAY CLEARANCE</option>
                                            <option value= "BUSINESS PERMIT">BUSINESS PERMIT</option>
                                            <option value= "CERTIFICATE OF INDIGENCY">CERTIFICATE OF INDIGENCY</option>
                                            <option value= "CERTIFICATE OF RESIDENCY">CERTIFICATE OF RESIDENCY</option>
                                        </select>
                                        <div @click="SelectCert" class="w-32 h-10 rounded-lg bg-amber-500 hover:bg-amber-300 text-center cursor-pointer text-xl text-white font-medium mx-3 mt-1 py-1">Continue</div>
                                </div>
                            </div>
                            <div v-if= "BrgyClearance" class="mt-3 px-5 w-full h-3/4 ">
                                <div class="w-full h-1/5 bg-teal-100 rounded text-left">
                                    <p class="font-bold text-blue-700 pt-3 ml-5 text-lg">BARANGAY CLEARANCE</p>
                                    <p class="font-bold text-neutral-800 pt-1 ml-10 text-base">Issued identification documents neededd for many important business job or personal transactions.</p>
                                </div>
                                <div class="mt-5 w-full h-3/4 rounded border-2">
                                    <div class="text-center">
                                        <p class="font-bold text-amber-500 pt-3 ml-5 text-lg">Please provide all the information below</p>
                                    </div>
                                    <div class="flex mt-5 text-left">
                                        <div class="grid grid-cols-1 px-3 w-1/4">
                                            <label class="uppercase md:text-sm text-xs text-gray-500 text-light font-semibold">First Name</label>
                                            <text class="py-2 px-3 rounded-lg border-2 border-teal-400 mt-1 focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent" type="text" >{{first}}</text>
                                        </div>
                                        <div class="grid grid-cols-1 px-3 w-1/4">
                                            <label class="uppercase md:text-sm text-xs text-gray-500 text-light font-semibold">Midle Name</label>
                                            <text class="py-2 px-3 rounded-lg border-2 border-teal-400 mt-1 focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent" type="text" >{{middle}}</text>
                                        </div>
                                        <div class="grid grid-cols-1 px-3 w-1/4">
                                            <label class="uppercase md:text-sm text-xs text-gray-500 text-light font-semibold">Last Name</label>
                                            <text class="py-2 px-3 rounded-lg border-2 border-teal-400 mt-1 focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent" type="text" >{{last}}</text>
                                        </div>
                                        <div class="grid grid-cols-1 px-3 w-1/4">
                                            <label class="uppercase md:text-sm text-xs text-gray-500 text-light font-semibold">Suffix</label>
                                            <text class="py-2 px-3 rounded-lg border-2 border-teal-400 mt-1 focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent" type="text" >{{suffix}}</text>
                                        </div>
                                    </div>
                                    <div class="flex mt-5 text-left">
                                        <div class="grid grid-cols-1 px-3 w-1/4">
                                            <label class="uppercase md:text-sm text-xs text-gray-500 text-light font-semibold">Purok</label>
                                            
                                            <text class="py-2 px-3 rounded-lg border-2 border-teal-400 mt-1 focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent" type="text" >{{purok}}</text>
                                        </div>
                                        <div class="grid grid-cols-1 px-3 w-1/4">
                                            <label class="uppercase md:text-sm text-xs text-gray-500 text-light font-semibold">Citizenship</label>
                                            <input v-model="iccitizenship" class="py-2 px-3 rounded-lg border-2 border-teal-400 mt-1 focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent" type="text" placeholder="Citizenship" />
                                        </div>
                                        <div class="grid grid-cols-1 px-3 w-1/4">
                                            <label class="uppercase md:text-sm text-xs text-gray-500 text-light font-semibold">Status</label>
                                            <input v-model="icstatus" class="py-2 px-3 rounded-lg border-2 border-teal-400 mt-1 focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent" type="text" placeholder="Status" />
                                        </div>
                                        <div class="grid grid-cols-1 px-3 w-1/4">
                                            <label class="uppercase md:text-sm text-xs text-gray-500 text-light font-semibold">Age</label>
                                            <input v-model="icage" class="py-2 px-3 rounded-lg border-2 border-teal-400 mt-1 focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent" type="text" placeholder="Age" />
                                        </div>
                                    </div>
                                    <div class="flex mt-5 text-left">
                                        <div class="grid grid-cols-1 px-3 w-1/4">
                                            <label class="uppercase md:text-sm text-xs text-gray-500 text-light font-semibold">Quantity</label>
                                            <input v-model="icquantity" class="py-2 px-3 rounded-lg border-2 border-teal-400 mt-1 focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent" type="text" placeholder="pcs" />
                                        
                                        </div>
                                        <div class="grid grid-cols-1 px-3 w-1/4">
                                            <label class="block mt-2 text-xs font-semibold text-gray-600 uppercase ml-2">Include Cedula</label>
                                            <select v-model="icedula" 
                                            class="py-2 px-3 rounded-lg border-2 border-teal-400 mt-1 focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent">
                                                <option value= "Yes">Yes</option>
                                                <option value= "No">No</option>
                                            </select>
                                        </div>
                                        <div class="absolute right-32 mt-10 flex">
                                            <div @click="ClearanceInfo" class="w-32 h-10 rounded-full bg-amber-500 hover:bg-amber-300 mt-3 text-center cursor-pointer text-xl text-white font-medium py-1 mr-2">Request</div> 
                                            <div @click="DateTime" class="w-32 h-10 rounded-full bg-amber-500 hover:bg-amber-300 mt-3 text-center cursor-pointer text-xl text-white font-medium py-1">Back</div> 
                                        </div>
                                    </div>
                                </div>
                            </div> 

                        </div>
                    </div> 
                    <div v-if ="OptionRevAppInfo" class="px-10 mt-5"> 
                        <div v-if ="clearance">
                                <h1 class="text-xl font-semibold text-left text-amber-600">Review Application Information</h1>
                                <form @submit.prevent="addclearance">
                                <div class="ml-10">
                                     <div class="flex mt-5">
                                        <p class="font-semibold text-justify text-cyan-600 text-lg">Type of Certificate:</p>
                                        <p class="font-semibold text-justify text-lg ml-2">Barangay Clearance</p>
                                    </div>
                                    <div class="flex mt-1">
                                        <p class="font-semibold text-justify text-lg text-cyan-600">Date and Time: </p>
                                        <text class="font-semibold text-justify text-lg ml-2"> {{date}} </text>
                                        <p class="font-semibold text-justify text-lg ml-2"> at </p>
                                        <text class="font-semibold text-justify text-lg ml-2"> {{time}} </text>
                                    </div>
                                     <div class="flex mt-1">
                                        <p class="font-semibold text-justify text-cyan-600 text-lg">First Name:</p>
                                        <text class="font-semibold text-justify text-lg ml-2"> {{first}} </text>
                                    </div>
                                     <div class="flex mt-1">
                                        <p class="font-semibold text-justify text-cyan-600 text-lg">Middle Name:</p>
                                        <text class="font-semibold text-justify text-lg ml-2"> {{middle}} </text>
                                    </div>
                                     <div class="flex mt-1">
                                        <p class="font-semibold text-justify text-cyan-600 text-lg">Last Name:</p>
                                        <text class="font-semibold text-justify text-lg ml-2"> {{last}} </text>
                                    </div>
                                     <div class="flex mt-1">
                                        <p class="font-semibold text-justify text-cyan-600 text-lg">Suffix :</p>
                                        <text class="font-semibold text-justify text-lg ml-2"> {{suffix}} </text>
                                    </div>
                                     <div class="flex mt-1">
                                        <p class="font-semibold text-justify text-cyan-600 text-lg">Purok :</p>
                                        <text class="font-semibold text-justify text-lg ml-2"> {{purok}} </text>
                                    </div>
                                     <div class="flex mt-1">
                                        <p class="font-semibold text-justify text-cyan-600 text-lg">Citizenship :</p>
                                        <text class="font-semibold text-justify text-lg ml-2"> {{iccitizenship}} </text>
                                    </div>
                                     <div class="flex mt-1">
                                        <p class="font-semibold text-justify text-cyan-600 text-lg">Status :</p>
                                        <text class="font-semibold text-justify text-lg ml-2"> {{icstatus}} </text>
                                    </div>
                                     <div class="flex mt-1">
                                        <p class="font-semibold text-justify text-cyan-600 text-lg">Age :</p>
                                        <text class="font-semibold text-justify text-lg ml-2">{{icage}} </text>
                                    </div>
                                     <div class="flex mt-1">
                                        <p class="font-semibold text-justify text-cyan-600 text-lg">Quantity :</p>
                                        <text class="font-semibold text-justify text-lg ml-2"> {{icquantity}}</text>
                                    </div>
                                     <div class="flex mt-1">
                                        <p class="font-semibold text-justify text-cyan-600 text-lg">With Cedula :</p>
                                        <text class="font-semibold text-justify text-lg ml-2"> {{icedula}}</text>
                                    </div>                                      
                                     <div class="mt-10 flex">
                                        <input type="submit" value="Confirm" class="w-32 h-10 rounded-full bg-amber-500 hover:bg-amber-300 mt-3 text-center cursor-pointer text-xl text-white font-medium py-1 mr-2"/> 
                                        <div @click="AppInfo" class="w-32 h-10 rounded-full bg-amber-500 hover:bg-amber-300 mt-3 text-center cursor-pointer text-xl text-white font-medium py-1">Back</div> 
                                    </div>
                                </div>      
                            </form>
                        </div> 
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

import { app } from "../firebase";
import { auth } from "../firebase";
import { getFirestore, getDoc, setDoc, doc } from "firebase/firestore";
export default {
    data(){
        return{

        first: '', middle: '', last: '', suffix: '', purok: '',

        ctype: '', ftype: '', date: 'Sample Date', time: 'Sample Time', totalcost: '',

        BrgyClearance: false, 
        BrgyPermit: false, 
        Residency: false, 
        Indigency: false,
        start: true, 
        OptionAppInfo: false, 
        OptionDateTime: false, 
        OptionRevAppInfo: false,
        dat1: true, dat2: false, 
        ai1: true, ai2: false,
        rai1: true, rai2: false,   

        clearance: false, 
        iccitizenship: '', icstatus: '', icage: '', icquantity: '', icedula: '',
        
        }
    },
     created(){
       this.loadresident();
     },
    methods:{
        async loadresident(){ 
           const db = getFirestore(app)
           const userid = auth.currentUser.uid;  
           const residentRef = doc(db, "residents",userid);
           const residentSnap = await getDoc(residentRef);  

           if(residentSnap.exists){
               console.log("Document data:", residentSnap.data());
               this.first = residentSnap.data().first;
               this.middle = residentSnap.data().middle;
               this.last = residentSnap.data().last;
               this.suffix = residentSnap.data().suffix;
               this.purok = residentSnap.data().purok;
           } else{
               console.log("No such document!");
           }

        },
      SelectCert(){
          
          if(this.ctype=='BARANGAY CLEARANCE'){
              this.ftype='BARANGAY CLEARANCE';
              this.BrgyClearance=true;
              this.BrgyPermit=false;
              this.Indigency=false;
              this.Residency=false;
          }
          else if (this.ctype=='BUSINESS PERMIT'){
              this.ftype='BUSINESS PERMIT';
              this.BrgyClearance=false;
              this.BrgyPermit=true;
              this.Indigency=false;
              this.Residency=false;
          }
          else if (this.ctype=='CERTIFICATE OF INDIGENCY'){
              this.ftype='CERTIFICATE OF INDIGENCY';
              this.BrgyClearance=false;
              this.BrgyPermit=false;
              this.Indigency=true;
              this.Residency=false;
          }
          else if (this.ctype=='CERTIFICATE OF RESIDENCY'){
              this.ftype='CERTIFICATE OF RESIDENCY';
              this.BrgyClearance=false;
              this.BrgyPermit=false;
              this.Indigency=false;
              this.Residency=true;
          }
          
      },
      DateTime(){
        this.OptionDateTime = true;
        this.OptionAppInfo = false;
        this.OptionRevAppInfo = false;
        this.start = false;

        this.dat1= false;
        this.ai1= true;
        this.rai1= true;
        this.dat2= true;
        this.ai2= false;
        this.rai2= false;

      },
      ClearanceInfo(){
        if(
            this.iccitizenship == '' ||
            this.icstatus == '' ||
            this.icage == '' ||
            this.icquantity == '' ||
            this.icedula == ''
            ){
                alert("Parameters cant be empty");
            }
        else if(this.ftype==this.ctype){
            this.clearance = true;
            this.OptionRevAppInfo = true;
            this.OptionDateTime = false;
            this.OptionAppInfo = false;
            this.start = false;

            this.dat1= true;
            this.ai1= true;
            this.rai1= false;
            this.dat2= false;
            this.ai2= false;
            this.rai2= true;        
        }
        else{
            alert("Click Continue before proceeding");
        }
      },
      AppInfo(){
        this.OptionDateTime = false;
        this.OptionAppInfo = true;
        this.OptionRevAppInfo = false;
        this.start = false;

        this.dat1= true;
        this.ai1= false;
        this.rai1= true;
        this.dat2= false;
        this.ai2= true;
        this.rai2= false;
      },
      async addclearance(){

        const BCdate = this.date;
        const BCtime = this.time;  
        const BCfirst = this.first;
        const BCmiddle = this.middle;
        const BClast = this.last;
        const BCsuffix = this.suffix;
        const BCpurok = this.purok;
        const BCcitizenship = this.iccitizenship;
        const BCstatus = this.icstatus;
        const BCage = this.icage;
        const BCquantity = this.icquantity;
        const BCcedula = this.icedula;

        const db = getFirestore(app);
        const currendID = auth.currentUser.uid;
        console.log("Creating Data");
        const addedDocs = await setDoc(doc(db, "Clearance Requests",currendID ),{currendID, BCdate, BCtime, BCfirst, BCmiddle, BClast, BCsuffix, BCpurok, BCcitizenship, BCstatus, BCage, BCquantity, BCcedula});
        alert("Document Added Successfully");
        console.log(addedDocs);

        this.$router.push("/homepage");
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
