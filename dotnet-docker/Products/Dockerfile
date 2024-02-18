# Pull the <mcr.microsoft.com/dotnet/sdk:8.0> image and name the image build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
# Set the working directory within the image to /DataEntities
WORKDIR /DataEntities
# Copy the file named DataEntities.csproj found locally to the </DataEntities> directory that you created
COPY "DataEntities/DataEntities.csproj" .
# Call <dotnet restore> on the project
RUN dotnet restore
# Copy everything in the local DataEntities directory to the image
COPY "DataEntities" .
# Call <dotnet publish> on the project
RUN dotnet publish -c release -o /app

# Set the working directory within the image to </src>
WORKDIR /src
 # Copy the file named <Products.csproj> found locally to the </src> directory that you created.
 COPY Products/Products.csproj .
 # Call <dotnet restore> on the project
 RUN dotnet restore
 # Copy everything in the local <Products> directory to the image
 COPY Products .
 # Call <dotnet publish> on the project
 RUN dotnet publish -c release -o /app

# Pull the <mcr.microsoft.com/dotnet/aspnet:8.0> image
FROM mcr.microsoft.com/dotnet/aspnet:8.0
# Set the working directory within the image to </app>
WORKDIR /app
# Expose port 80 and 443
EXPOSE 80
EXPOSE 443
# Copy everything from the <app> directory of the <build> image you created into the <app> directory of this image
COPY --from=build /app .
# Set the entry point of this image to <dotnet> and pass <Products.dll> as an argument
ENTRYPOINT ["dotnet", "Products.dll"]