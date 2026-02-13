Disk Recovery - rozszerzenie dysku C
Źródło=https://thedxt.ca/2023/06/moving-windows-recovery-partition-correctly/ 

[Nagranie z modyfikacji dysku Recovery] (https://www.youtube.com/watch?v=Ra6vUOsLNQU)

Kroki do wykonania
1) Wyłączenie Windows Recovery Partition

reagentc /disable

2) Przejście do działań w ramach DiskPart
   
diskpart

	2.1)Wylistowanie dysków
   	
	list disk
	
	2.2) Wybranie dysku
	
	select disk "X"
	
	2.3) Wylistowanie partycji w ramach wybranego dysku
	
	list partition
	
	2.4) Wybranie partycji do usunięcia
	
	select partition "Y"
	
	2.5) Skasowanie partycji
	
	delete partition override

4) Rozszerzenie dysku C o niezbędną wielkość oraz pozostawienie 1GB na utworzenie nowej partycji Receovery.
Jeśli zdarzy się że zapomnimy pozostawić wolną przestrzeń doprowadzamy do stanu w którym mamy 1 GB wolnej przestrzeni.

5) Tworzymy nową partycję recovery
	4.1) klikamy na wolnej przestrzeni prawym przyciskiem myszy i wybieramy "New Simple Volume"
	4.2) w nowym oknie wybieramy "Do not assign a drive letter or drive path" i klikamy Next
	4.3) w nowym oknie nadajemy nazwę np. "New Recovery" i klikamy Next

6) Ponownie wracamy do diskpart
	5.1) wybieramy nowo utworzoną partycję
	
	select partition "id nowej partycji

	5.2)nadajemy odpowiedni ID
		5.2.1 Gdy dysk jest w trybie GPT
	
		set id=de94bba4-06d1-4d40-a16a-bfd50179d6ac

		dodatkowo ukrywamy partycję

		gpt attributes=0x8000000000000001

		5.2.2 Gdy dysk jest w trybie MBR 

		set id=27

	5.3) Wychodzimy z diskpart
	
	exit

6)Włączamy Windows Recovery Partition

reagentc /enable
