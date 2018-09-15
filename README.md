# Simulated-Annealing
Berisi tugas AI
function operasi(){ //fungsi yang dibuat untuk mengacak operasi untuk menentukan nilai X1current berikutnya
	let x1 = Math.random();
	
	if(x1>=0.5){
		var op = "minus";
	}else{
		var op = "plus";
	}

	return op;

}

function generate(){ //fungsi simulated anealing.
	var opr = operasi();

	let X1curr = 0; //current state
	let X2curr = 0; 
	let t = 100; //temprature
	const g = -9; //nilai negatif
	let e = Math.E;

	let X1best = X1curr; //simpan best
	let X2best = X2curr;
	let Ebest = soal(X1best, X2best); //simpan nilai terbaik

	while(t!= 0){ //Looping Simulated anealing


		if((X1curr  < 9 && X2curr < 9) && (X1curr > g && X2curr > g)){ //in range

			if(opr == "plus"){ //Jika hasil operasi untuk menggerakkan X1 & X2 current adalah tambah 
				let Ecurr = soal(X1curr, X2curr); //simpan current energi
				

				X2curr = X2curr + Math.random();
				X1curr = X1curr - Math.random(); 

				let X1new = X1curr; //simpan nilai terbaru
				let X2new = X2curr;

				let Enew = soal(X1new, X2new);

				let deltaE = Enew - Ecurr; //delta E

					if(deltaE < 0) {
						X1curr = X1new;
						X2curr = X2new;
						 if(Enew < Ebest){
						 	X1best = X1new;
						 	X2best = X2new;
						 	Ebest = Enew;
						 }else{
						 	let pangkat = -(deltaE/t);
						 	let P = Math.pow(e,pangkat);

						 	let R = Math.random;
						 		if(R<P){
						 			X1curr = X1new;
						 			X2curr = X2new;
						 		}

						 }

					}

			}

			else{

				let Ecurr = soal(X1curr, X2curr); //simpan current energi
				

				X2curr  = X2curr  - Math.random()
				X1curr = X1curr + Math.random();

				let X1new = X1curr; //simpan nilai terbaru
				let X2new = X2curr;

				let Enew = soal(X1new, X2new);

				let deltaE = Enew - Ecurr; //Delta E

				if(deltaE < 0) {
						X1curr = X1new;
						X2curr = X2new;
						 if(Enew < Ebest){
						 	X1best = X1new;
						 	X2best = X2new;
						 	Ebest = Enew;
						 }else{
						 	let pangkat = -(deltaE/t);
						 	let P = Math.pow(e,pangkat);

						 	let R = Math.random;
						 		if(R<P){
						 			X1curr = X1new;
						 			X2curr = X2new;
						 		}

						 }

					}


			}

		}

		//Akhir loop
		t = t-1;
	}
	
	var energi = [X1curr, X2curr, Ebest];
	return energi;
	
}


Math.radians = function(degrees) { //fungsi radian
  return degrees * Math.PI / 180;
};

function soal(x1,x2){ //fungsi mengenarate soal ke bahasa pemrograman.
	let a = Math.sin(Math.radians(x1)); //variabel biasa
	let b = Math.cos(Math.radians(x2));

	let a2 = Math.pow(x1, 2); // variabel kuadrat
	let b2 = Math.pow(x2, 2);

	let tot = a2 + b2; //hasil penjumlahan kuadrat

	let sqr = Math.sqrt(tot); // hasil akar kuadrat dari penjumlahan x1^2 ditambah x2^2

	let pi = Math.PI; // nilai pi 3.14

	let has = sqr/pi; //hasil operasi akar kuadrat dibagi pi.

	let isiEksponen = 1 - has;

	let isiEksponenMultak = Math.abs(isiEksponen);

	let exp = Math.exp(isiEksponenMultak); //hasil operasi dari exp();

	let hasil = a*b*exp; //hasil kali sin(x1)cos(x2)exp()

	let hasilAkhir = -Math.abs(hasil); //harga multak dari hasil dan dikali minus.

	return hasilAkhir;
	
		
}

//MAIN PROGRAM.

	var goal = generate();
		alert("X1 = "+ goal[0] +"\n"
		+"X2 = "+ goal[1] +"\n"
	 	+"Hasil = "+ goal[2]);


