LABNAME = Multiple modules
SMOKENAME = Tb

BSC=bsc -no-show-timestamps -no-show-version

## Default simulator is iverilog
VSIM = -vsim iverilog

ifdef modelsim
    VSIM = -vsim modelsim
endif

.PRECIOUS: mk%.v

.PHONY: clean
clean:
	@rm -f *.bi *.bo *.ba 
	@rm -f *.cxx *.h *.o *.so *.bexe
	@rm -f *.v *.vexe
	@rm -f *.vcd *~ *.fsdb *.log
	@rm -rf csrc INCA_libs simv.daidir vfastLog/ nWaveLog/ work_mkTb/

.PHONY: smoke_test
smoke_test: smoke_test_verilog smoke_test_bluesim

.PHONY:	smoke_test_verilog
smoke_test_verilog: clean
	@echo ""
	@echo "Checking Verilog generation"
	$(BSC) -verilog $(SMOKENAME).bsv
	@echo ""
	@echo "Checking Verilog simulation"
	$(BSC) $(VSIM) -e mk$(SMOKENAME) -o mk$(SMOKENAME).vexe mk$(SMOKENAME).v
	./mk$(SMOKENAME).vexe
	@echo ""

.PHONY: smoke_test_bluesim
smoke_test_bluesim: clean
	@echo ""
	@echo "Checking bsc compiles"
	$(BSC) -sim $(SMOKENAME).bsv
	@echo ""
	@echo "Checking compile for Bluespec simulator"	
	$(BSC) -sim -o mk$(SMOKENAME).bexe -e mk$(SMOKENAME) mk$(SMOKENAME).ba
	./mk$(SMOKENAME).bexe
	@echo ""
