# Carpark
car parking ticket system for 20 slots


Experiment 1: LED Lighting​

library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity led_on is
    Port ( led : out STD_LOGIC );
end led_on;

architecture Behavioral of led_on is
begin
    led <= '1'; -- LED is always ON
end Behavioral;


NET "led" LOC = "P45";  # Assign the correct pin number for the LED




Experiment 3: Button-Controlled LED

library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity ButtonLED is
    Port ( 
        button : in STD_LOGIC;
        led : out STD_LOGIC
    );
end ButtonLED;

architecture Behavioral of ButtonLED is
begin
    led <= button;  -- LED follows the button state
end Behavioral;


NET "led" LOC = "P45";       # LED pin
NET "button" LOC = "P30";    # Button pin (Adjust as per board)



Experiment 4: 4-bit Counter using FPGA Clock and LEDs

library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.STD_LOGIC_ARITH.ALL;
use IEEE.STD_LOGIC_UNSIGNED.ALL;

entity counter_4bit is
    Port ( 
        clk : in  STD_LOGIC;           -- Clock input
        rst : in  STD_LOGIC;           -- Reset input
        count_out : out STD_LOGIC_VECTOR (3 downto 0)  -- Output to LEDs
    );
end counter_4bit;

architecture Behavioral of counter_4bit is
    signal count : STD_LOGIC_VECTOR(3 downto 0) := "0000";
begin
    process(clk, rst)
    begin
        if rst = '1' then
            count <= "0000";
        elsif rising_edge(clk) then
            count <= count + 1;
        end if;
    end process;

    count_out <= count;
end Behavioral;


NET "clk" LOC = P85 | IOSTANDARD = LVCMOS33;  -- Clock
NET "rst" LOC = P86 | IOSTANDARD = LVCMOS33;  -- Reset

NET "count_out<0>" LOC = P40 | IOSTANDARD = LVCMOS33;  -- LED1
NET "count_out<1>" LOC = P41 | IOSTANDARD = LVCMOS33;  -- LED2
NET "count_out<2>" LOC = P42 | IOSTANDARD = LVCMOS33;  -- LED3
NET "count_out<3>" LOC = P43 | IOSTANDARD = LVCMOS33;  -- LED4