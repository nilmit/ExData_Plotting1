ExData_Plotting1
================

Project

#Program week1 from dataset household_power_consumption.txt
 
if(!file.exists("exdata-data-household_power_consumption.zip")) {
         temp <- tempfile()
         download.file("http://d396qusza40orc.cloudfront.net/exdata%2Fdata%2Fhousehold_power_consumption.zip",temp)
         file <- unzip(temp)
         unlink(temp)
 }

 power <- read.table(file, header=T, sep=";")
 power$Date <- as.Date(power$Date, format="%d/%m/%Y")
 sdatafile <- power[(power$Date=="2007-02-01") | (power$Date=="2007-02-02"),]
 sdatafile$Global_active_power <- as.numeric(as.character(sdatafile$Global_active_power))
 sdatafile$Global_reactive_power <- as.numeric(as.character(sdatafile$Global_reactive_power))
 sdatafile$Voltage <- as.numeric(as.character(sdatafile$Voltage))
 sdatafile <- transform(sdatafile, timestamp=as.POSIXct(paste(Date, Time)), "%d/%m/%Y %H:%M:%S")
 sdatafile$Sub_metering_1 <- as.numeric(as.character(sdatafile$Sub_metering_1))
 sdatafile$Sub_metering_2 <- as.numeric(as.character(sdatafile$Sub_metering_2))
 sdatafile$Sub_metering_3 <- as.numeric(as.character(sdatafile$Sub_metering_3))

#############################################
#PLOT 1
#############################################
plot1 <- function() {
   par(mfrow=c(1,1))
        hist(sdatafile$Global_active_power, main = paste("Global Active Power"), col="red", xlab="Global Active Power (kilowatts)")
        dev.copy(png, file="plot1.png", width=480, height=480)
        dev.off()
        cat("Plot1.png saved in", getwd())
}
plot1()
#############################################
#PLOT 2
#############################################
plot2 <- function() {
    par(mfrow=c(1,1))
     plot(sdatafile$timestamp, sdatafile$Global_active_power, type="l", xlab="", ylab="Global Active Power (kilowatts)")
         dev.copy(png, file="plot2.png", width=480, height=480)
         dev.off()
         cat("plot2.png saved in", getwd())
 }
plot2()

##############################################
#PLOT 3
##############################################
plot3 <- function() {
   par(mfrow=c(1,1))
         plot(sdatafile$timestamp,sdatafile$Sub_metering_1, type="l", xlab="", ylab="Energy sub metering")
         lines(sdatafile$timestamp,sdatafile$Sub_metering_2,col="red")
         lines(sdatafile$timestamp,sdatafile$Sub_metering_3,col="blue")
         legend("topright", col=c("black","red","blue"), c("Sub_metering_1  ","Sub_metering_2  ", "Sub_metering_3  "),lty=c(1,1), lwd=c(1,1))
         dev.copy(png, file="plot3.png", width=480, height=480)
         dev.off()
         cat("plot3.png saved in", getwd())
 }
plot3()

##############################################
#PLOT 4
##############################################
plot4 <- function() {
         par(mfrow=c(2,2))         


         plot(sdatafile$timestamp, sdatafile$Global_active_power, type="l", xlab="", ylab="Global Active Power")


         plot(sdatafile$timestamp, sdatafile$Voltage, type="l", xlab="datetime", ylab="Voltage")
         

         plot(sdatafile$timestamp, sdatafile$Sub_metering_1, type="l", xlab="", ylab="Energy sub metering")
         lines(sdatafile$timestamp, sdatafile$Sub_metering_2,col="red")
         lines(sdatafile$timestamp, sdatafile$Sub_metering_3,col="blue")
         legend("topright", col=c("black","red","blue"), c("Sub_metering_1  ","Sub_metering_2  ", "Sub_metering_3  "),lty=c(1,1), bty="n", cex=.5)    

         plot(sdatafile$timestamp, sdatafile$Global_reactive_power, type="l", xlab="datetime", ylab="Global_reactive_power")
         
#OUTPUT
         dev.copy(png, file="plot4.png", width=480, height=480)
         dev.off()
         cat("plot4.png saved in", getwd())
}
plot4()

![GitHub Logo] (https://github.com/nilmit/ExData_Plotting1/issues)
![GitHub Logo] (https://github.com/nilmit/ExData_Plotting1/issues)
