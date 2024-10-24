<template>
  <div class="min-h-screen bg-neutral-300/70">
    <Form
      v-slot="{ meta }"
      :validation-schema="toTypedSchema(formSchema[currentStep])"
      :initial-values="formData"
      @submit="submitForm"
      class="h-screen flex"
    >
      <!-- Stepper Section -->
      <div class="w-[350px] bg-gray-100 border-r shadow-md shadow-blue-300/10">
        <ScrollArea class="h-full">
          <div class="p-8 pt-14">
            <div class="flex flex-col gap-2">
              <div 
                v-for="(step, index) in steps" 
                :key="index" 
                class="relative flex items-start gap-6 mb-4"
              >
                <div 
                  class="absolute left-[18px] top-[38px] block h-[calc(100%-20px)] w-0.5 shrink-0 rounded-full bg-muted" 
                  v-if="index !== steps.length - 1"
                />
                <Button
                  @click="currentStep = index"
                  :variant="currentStep >= index ? 'default' : 'outline'"
                  size="icon"
                  class="z-10 rounded-full shrink-0"
                  :class="[currentStep === index && 'ring-2 ring-ring ring-offset-2 ring-offset-background bg-blue-900']"
                >
                  <CheckIcon v-if="currentStep > index" class="size-5" />
                  <CircleIcon v-if="currentStep === index" />
                  <DotIcon v-if="currentStep < index" />
                </Button>
                <div class="mt-3 mb-6">
                  <span 
                    :class="[currentStep === index && 'text-primary']" 
                    class="text-sm font-semibold transition lg:text-base"
                  >
                    {{ step }}
                  </span>
                </div>
              </div>
            </div>
          </div>
        </ScrollArea>
      </div>

      <!-- Form Section -->
      <div class="flex-1 flex flex-col h-full overflow-hidden">
        <main class="flex-1 overflow-y-auto p-8">
          <div class="max-w-3xl mx-auto">
            <CustomProgressBar 
              :value="currentStep + 1" 
              :max="steps.length" 
              class="w-full mb-4" 
            />
            
            <Card class="shadow-lg">
              <CardContent class="p-6">
                <transition name="slide" mode="out-in">
                  <div :key="currentStep">
                    <!-- Step 1 -->
                    <div class="flex flex-col gap-2" v-if="currentStep === 0">
                      <h2 class="text-lg font-semibold text-black-900">Subject Property</h2>
                      <hr class="w-full border-t border-gray-300 mb-2">

                      <FormField v-slot="{ field }" name="propertyAddress">
                        <FormItem>
                          <FormLabel>Property Address</FormLabel>
                          <FormControl>
                            <Input v-model="formData.propertyAddress" v-bind="field" 
                              class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                     focus:outline-none focus:border-blue-400/50 
                                     hover:border-gray-400 bg-white border-gray-300"
                              placeholder="Property Address"/>
                          </FormControl>
                          <FormMessage />
                        </FormItem>
                      </FormField>

                      <FormField v-slot="{ field }" name="municipality">
                        <FormItem>
                          <FormLabel>Municipality</FormLabel>
                          <FormControl>
                            <Input v-model="formData.municipality" v-bind="field" 
                              class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                     focus:outline-none focus:border-blue-400/50 
                                     hover:border-gray-400 bg-white border-gray-300"
                              placeholder="Municipality"/>
                          </FormControl>
                          <FormMessage />
                        </FormItem>
                      </FormField>

                      <FormField v-slot="{ field }" name="county">
                        <FormItem>
                          <FormLabel>County</FormLabel>
                          <FormControl>
                            <Input v-model="formData.county" v-bind="field" 
                              class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                     focus:outline-none focus:border-blue-400/50 
                                     hover:border-gray-400 bg-white border-gray-300"
                              placeholder="County"/>
                          </FormControl>
                          <FormMessage />
                        </FormItem>
                      </FormField>

                      <FormField v-slot="{ field }" name="state">
                        <FormItem>
                          <FormLabel>State</FormLabel>
                          <FormControl>
                            <Input v-model="formData.state" v-bind="field" 
                              class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                     focus:outline-none focus:border-blue-400/50 
                                     hover:border-gray-400 bg-white border-gray-300" 
                              placeholder="State"/>
                          </FormControl>
                          <FormMessage />
                        </FormItem>
                      </FormField>

                      <FormField v-slot="{ field }" name="assessorParcelNumber">
                        <FormItem>
                          <FormLabel>Assessor Parcel Number</FormLabel>
                          <FormControl>
                            <Input v-model="formData.assessorParcelNumber" v-bind="field" 
                              class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                     focus:outline-none focus:border-blue-400/50 
                                     hover:border-gray-400 bg-white border-gray-300" 
                              placeholder="Assessor Parcel Number" />
                          </FormControl>
                          <FormMessage />
                        </FormItem>
                      </FormField>

                      <FormField v-slot="{ field }" name="yearBuilt">
                        <FormItem>
                          <FormLabel>Year Built</FormLabel>
                          <FormControl>
                            <Input
                              type="number"
                              v-model="formData.yearBuilt"
                              v-bind="field"
                              class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                    focus:outline-none focus:border-blue-400/50 
                                    hover:border-gray-400 bg-white border-gray-300"
                              placeholder="Year Built"
                              :min="1900"
                              :max="new Date().getFullYear()"
                            />
                          </FormControl>
                          <FormMessage />
                        </FormItem>
                      </FormField>

                      <FormField v-slot="{ field }" name="existingLandUse">
                        <FormItem>
                          <FormLabel>Existing Land Use</FormLabel>
                          <FormControl>
                            <Input v-model="formData.existingLandUse" v-bind="field" 
                              class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                     focus:outline-none focus:border-blue-400/50 
                                     hover:border-gray-400 bg-white border-gray-300" 
                              placeholder="Existing Land Use" />
                          </FormControl>
                          <FormMessage />
                        </FormItem>
                      </FormField>
                    </div>

                    <!-- Step 2 -->
                    <div class="flex flex-col gap-2" v-if="currentStep === 1">
                      <h2 class="text-lg font-semibold text-black-900">Zoning District</h2>
                      <hr class="w-full border-t border-gray-300 mb-2">

                      <FormField v-slot="{ field }" name="zoningJurisdiction">
                        <FormItem>
                          <FormLabel>Zoning Jurisdiction</FormLabel>
                          <FormControl>
                            <Input v-model="formData.zoningJurisdiction" v-bind="field" 
                              class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                     focus:outline-none focus:border-blue-400/50 
                                     hover:border-gray-400 bg-white border-gray-300" 
                              placeholder="Zoning Jurisdiction"/>
                          </FormControl>
                          <FormMessage />
                        </FormItem>
                      </FormField>

                      <FormField v-slot="{ field }" name="zoningDistrict">
                        <FormItem>
                          <FormLabel>Zoning District</FormLabel>
                          <FormControl>
                            <Input v-model="formData.zoningDistrict" v-bind="field" 
                              class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                     focus:outline-none focus:border-blue-400/50 
                                     hover:border-gray-400 bg-white border-gray-300" 
                              placeholder="Zoning District"/>
                          </FormControl>
                          <FormMessage />
                        </FormItem>
                      </FormField>

                      <FormField v-slot="{ field }" name="overlayDistrict">
                        <FormItem>
                          <FormLabel>Overlay District (optional)</FormLabel>
                          <FormControl>
                            <Input v-model="formData.overlayDistrict" v-bind="field" 
                              class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                     focus:outline-none focus:border-blue-400/50 
                                     hover:border-gray-400 bg-white border-gray-300" 
                              placeholder="Overlay District"/>
                          </FormControl>
                          <FormMessage />
                        </FormItem>
                      </FormField>

                      <FormField v-slot="{ field }" name="overlayZone">
                        <FormItem>
                          <FormLabel>Overlay Zone (optional)</FormLabel>
                          <FormControl>
                            <Input v-model="formData.overlayZone" v-bind="field" 
                              class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                     focus:outline-none focus:border-blue-400/50 
                                     hover:border-gray-400 bg-white border-gray-300" 
                              placeholder="Overlay Zone"/>
                          </FormControl>
                          <FormMessage />
                        </FormItem>
                      </FormField>

                      <h2 class="text-lg font-semibold text-black-900 mt-4">Date of Existing Ordinance</h2>
                      <hr class="w-full border-t border-gray-300 mb-2">

                      <FormField v-slot="{ field }" name="adoptedDate">
                        <FormItem>
                          <FormLabel>Adopted Date</FormLabel>
                          <FormControl>
                            <Input
                              type="number"
                              v-model="formData.adoptedDate"
                              v-bind="field"
                              class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                    focus:outline-none focus:border-blue-400/50 
                                    hover:border-gray-400 bg-white border-gray-300"
                              placeholder="Adopted Date"
                              :min="1900"
                              :max="new Date().getFullYear()"
                            />
                          </FormControl>
                          <FormMessage />
                        </FormItem>
                      </FormField>

                      <FormField v-slot="{ field }" name="amendedDate">
                        <FormItem>
                          <FormLabel>Amended Date (optional)</FormLabel>
                          <FormControl>
                            <Input
                              type="number"
                              v-model="formData.amendedDate"
                              v-bind="field"
                              class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                    focus:outline-none focus:border-blue-400/50 
                                    hover:border-gray-400 bg-white border-gray-300"
                              placeholder="Amended Date (optional)"
                              :min="1900"
                              :max="new Date().getFullYear()"
                            />
                          </FormControl>
                          <FormMessage />
                        </FormItem>
                      </FormField>

                      <FormField v-slot="{ field }" name="step2UsePermitted">
                        <FormItem>
                          <FormLabel class="text-md mb-2 mt-6">Is the Current Use Permitted?</FormLabel>
                          <FormControl>
                            <ToggleGroup v-model="formData.step2UsePermitted" type="single" v-bind="field" class="flex gap-4">
                              <ToggleGroupItem 
                                value="Yes" 
                                :class="{'selected': formData.step2UsePermitted === 'Yes'}"
                                class="toggle-group-item mt-1 p-2 w-full border border-gray-300 rounded-md text-[16px] shadow-sm focus:outline hover:border-gray-400"
                              >
                                Yes
                              </ToggleGroupItem>
                              <ToggleGroupItem 
                                value="No" 
                                :class="{'selected': formData.step2UsePermitted === 'No'}"
                                class="toggle-group-item mt-1 p-2 w-full border border-gray-300 rounded-md text-[16px] shadow-sm focus:outline hover:border-gray-400"
                              >
                                No
                              </ToggleGroupItem>
                            </ToggleGroup>
                          </FormControl>
                          <FormMessage />
                        </FormItem>
                      </FormField>

                      <FormField v-slot="{ field }" name="step2why">
                        <FormItem>
                          <FormLabel>Why</FormLabel>
                          <FormControl>
                            <Input v-model="formData.step2why" v-bind="field"
                              class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                     focus:outline-none focus:border-blue-400/50 
                                     hover:border-gray-400 bg-white border-gray-300" 
                              placeholder="Type Here"/>
                          </FormControl>
                          <FormMessage />
                        </FormItem>
                      </FormField>

                      <FormField v-slot="{ field }" name="step2UseConforming">
                        <FormItem>
                          <FormLabel class="text-md mb-2 mt-6">Is the Current Use Conforming?</FormLabel>
                          <FormControl>
                            <ToggleGroup v-model="formData.step2UseConforming" type="single" v-bind="field" class="flex gap-4">
                              <ToggleGroupItem 
                                value="Yes" 
                                :class="{'selected': formData.step2UseConforming === 'Yes'}"
                                class="toggle-group-item mt-1 p-2 w-full border border-gray-300 rounded-md text-[16px] shadow-sm focus:outline hover:border-gray-400"
                              >
                                Yes
                              </ToggleGroupItem>
                              <ToggleGroupItem 
                                value="No" 
                                :class="{'selected': formData.step2UseConforming === 'No'}"
                                class="toggle-group-item mt-1 p-2 w-full border border-gray-300 rounded-md text-[16px] shadow-sm focus:outline hover:border-gray-400"
                              >
                                No
                              </ToggleGroupItem>
                            </ToggleGroup>
                          </FormControl>
                          <FormMessage />
                        </FormItem>
                      </FormField>

                    </div>

                    <!-- Step 3 -->
                    <div class="flex flex-col gap-2" v-if="currentStep === 2">
                      <h2 class="text-lg font-semibold text-black-900">Adjacent Zoning</h2>
                      <hr class="w-full border-t border-gray-300 mb-2">

                      <h3 class="text-md font-semibold text-gray-900">North</h3>
                      <div class="flex justify-between items-baseline gap-x-6">
                        <div class="w-1/2">
                          <FormField v-slot="{ field }" name="zoningNorth">
                            <FormItem>
                              <FormLabel>Zoning</FormLabel>
                              <FormControl>
                                <Input v-model="formData.zoningNorth" v-bind="field" 
                                  class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                    focus:outline-none 
                                    hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300" 
                                  placeholder="Zoning"/>
                              </FormControl>
                              <FormMessage />
                            </FormItem>
                          </FormField>
                        </div>
                        <div class="w-1/2">
                          <FormField v-slot="{ field }" name="zoningDistrictNorth">
                            <FormItem>
                              <FormLabel>Zoning District</FormLabel>
                              <FormControl>
                                <Input v-model="formData.zoningDistrictNorth" v-bind="field" 
                                  class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                    focus:outline-none 
                                    hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300" 
                                  placeholder="Zoning District" />
                              </FormControl>
                              <FormMessage />
                            </FormItem>
                          </FormField>
                        </div>
                      </div>

                      <h3 class="text-md font-semibold text-gray-900 mt-4">South</h3>
                      <div class="flex justify-between items-baseline gap-x-6">
                        <div class="w-1/2">
                          <FormField v-slot="{ field }" name="zoningSouth">
                            <FormItem>
                              <FormLabel>Zoning</FormLabel>
                              <FormControl>
                                <Input v-model="formData.zoningSouth" v-bind="field" 
                                  class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                    focus:outline-none 
                                    hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300" 
                                  placeholder="Zoning"/>
                              </FormControl>
                              <FormMessage />
                            </FormItem>
                          </FormField>
                        </div>
                        <div class="w-1/2">
                          <FormField v-slot="{ field }" name="zoningDistrictSouth">
                            <FormItem>
                              <FormLabel>Zoning District</FormLabel>
                              <FormControl>
                                <Input v-model="formData.zoningDistrictSouth" v-bind="field" 
                                  class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                    focus:outline-none 
                                    hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300" 
                                  placeholder="Zoning District" />
                              </FormControl>
                              <FormMessage />
                            </FormItem>
                          </FormField>
                        </div>
                      </div>

                      <h3 class="text-md font-semibold text-gray-900 mt-4">East</h3>
                      <div class="flex justify-between items-baseline gap-x-6">
                        <div class="w-1/2">
                          <FormField v-slot="{ field }" name="zoningEast">
                            <FormItem>
                              <FormLabel>Zoning</FormLabel>
                              <FormControl>
                                <Input v-model="formData.zoningEast" v-bind="field" 
                                  class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                    focus:outline-none 
                                    hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300" 
                                  placeholder="Zoning"/>
                              </FormControl>
                              <FormMessage />
                            </FormItem>
                          </FormField>
                        </div>
                        <div class="w-1/2">
                          <FormField v-slot="{ field }" name="zoningDistrictEast">
                            <FormItem>
                              <FormLabel>Zoning District</FormLabel>
                              <FormControl>
                                <Input v-model="formData.zoningDistrictEast" v-bind="field" 
                                  class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                    focus:outline-none 
                                    hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300" 
                                  placeholder="Zoning District" />
                              </FormControl>
                              <FormMessage />
                            </FormItem>
                          </FormField>
                        </div>
                      </div>

                      <h3 class="text-md font-semibold text-gray-900 mt-4">West</h3>
                      <div class="flex justify-between items-baseline gap-x-6">
                        <div class="w-1/2">
                          <FormField v-slot="{ field }" name="zoningWest">
                            <FormItem>
                              <FormLabel>Zoning</FormLabel>
                              <FormControl>
                                <Input v-model="formData.zoningWest" v-bind="field" 
                                  class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                    focus:outline-none 
                                    hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300" 
                                  placeholder="Zoning"/>
                              </FormControl>
                              <FormMessage />
                            </FormItem>
                          </FormField>
                        </div>
                        <div class="w-1/2">
                          <FormField v-slot="{ field }" name="zoningDistrictWest">
                            <FormItem>
                              <FormLabel>Zoning District</FormLabel>
                              <FormControl>
                                <Input v-model="formData.zoningDistrictWest" v-bind="field" 
                                  class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                    focus:outline-none 
                                    hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300" 
                                  placeholder="Zoning District" />
                              </FormControl>
                              <FormMessage />
                            </FormItem>
                          </FormField>
                        </div>
                      </div>

                      <h2 class="text-lg font-semibold text-gray-900 mb-2 mt-6">Parcel Area</h2>
                      <hr class="w-full border-t border-gray-300 mb-2">

                      <div class="flex justify-between items-baseline gap-x-6">
                        <div class="w-1/2">
                          <FormField v-slot="{ field }" name="parcelArea">
                            <FormItem>
                              <FormLabel>Parcel Area</FormLabel>
                              <FormControl>
                                <Input v-model="formData.parcelArea" v-bind="field" 
                                  class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                    focus:outline-none 
                                    hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300" 
                                  placeholder="Parcel Area"/>
                              </FormControl>
                              <FormMessage />
                            </FormItem>
                          </FormField>
                        </div>
                        <div class="w-1/2">
                          <FormField v-slot="{ field }" name="parcelAreaUnit">
                            <FormItem>
                              <FormLabel>Unit</FormLabel>
                              <FormControl>
                                <Input v-model="formData.parcelAreaUnit" v-bind="field" 
                                  class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                    focus:outline-none 
                                    hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300" 
                                  placeholder="Unit"/>
                              </FormControl>
                              <FormMessage />
                            </FormItem>
                          </FormField>
                        </div>
                      </div>
                    </div>

                    <!-- Step 4 -->                    
                    <div class="flex flex-col gap-2" v-if="currentStep === 3">
                      
                      <!-- Building Setback Requirements -->
                      <h2 class="text-lg font-semibold text-gray-900 mb-2 mt-6">Building Setback Requirements</h2>
                      <hr class="w-full border-t border-gray-300 mb-4">
                      
                      <FormField v-slot="{ field }" name="step4Per">
                        <FormItem>
                          <FormLabel>Per</FormLabel>
                          <FormControl>
                            <Input v-model="formData.step4Per" v-bind="field" 
                            class="mt-1 p-2 pt-1 w-1/2 border rounded-md text-[16px] shadow-sm 
                            focus:outline-none 
                            hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300" 
                            placeholder="Per"/>
                          </FormControl>
                        </FormItem>
                      </FormField>
                      
                      <!--card row component-->
                      <h2 class="text-lg font-semibold text-gray-900 mb-2 mt-6">Minimum Front from Street</h2>
                      <hr class="w-full border-t border-gray-300 mb-4">
                      
                      <div class="flex flex-col sm:flex-row sm:space-x-4">

                        <!--required-->
                        <div class="flex flex-col w-full sm:w-1/2 p-2 pt-1 pb-4 border-2 rounded-md border-[#e0e0e0] shadow-none hover:shadow-lg flex-shrink pt-2">
                          <FormField v-slot="{ field }" name="requiredFeetFront.value1">
                            <FormItem>
                              <FormLabel>Required</FormLabel>
                              <FormControl>
                                <Input v-model="formData.requiredFeetFrontvalue1" v-bind="field" 
                                  class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                        focus:outline-none 
                                        hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300" 
                                  placeholder="Feet"/>
                              </FormControl>
                            </FormItem>
                        </FormField>
                        <Separator label="Or" class="mt-4 mb-2 bg-gray-400/50 font-medium " /> 
                        <FormField v-slot="{ field }" name="requiredFeetFront.value2">
                          <FormItem>
                            <FormControl> 
                              <Input v-model="formData.requiredFeetFrontvalue2" v-bind="field"  
                                class="mt-3 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                  focus:outline-none 
                                  hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300"
                                  placeholder="Type Here"/>
                            </FormControl>
                          </FormItem>
                        </FormField>
                        </div>


                        <!--existing -->
                        <div class="flex flex-col w-full sm:w-1/2 p-2 pt-1 pb-4 border-2 rounded-md border-[#e0e0e0] shadow-none hover:shadow-lg flex-shrink pt-2">
                          <FormField v-slot="{ field }" name="existingFeetFront.value1">
                            <FormItem>
                              <FormLabel>Existing</FormLabel>
                              <FormControl>
                                <Input v-model="formData.existingFeetFrontvalue1" v-bind="field" 
                                  class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                        focus:outline-none 
                                        hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300" 
                                  placeholder="Feet"/>
                              </FormControl>
                            </FormItem>
                        </FormField>
                        <Separator label="Or" class="mt-4 mb-2 bg-gray-400/50 font-medium " /> 
                        <FormField v-slot="{ field }" name="existingFeetFront.value2">
                          <FormItem>
                            <FormControl> 
                              <Input v-model="formData.existingFeetFrontvalue2" v-bind="field"  
                                class="mt-3 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                  focus:outline-none 
                                  hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300"
                                  placeholder="Type Here"/>
                            </FormControl>
                          </FormItem>
                        </FormField>
                      </div>
                      <!--end of existing-->
                      </div>
                      <!--end of card row component-->

                      <!--card row component-->
                      <h2 class="text-lg font-semibold text-gray-900 mb-2 mt-6">Minimum Corner Side</h2>
                      <hr class="w-full border-t border-gray-300 mb-4">
                      
                      <div class="flex flex-col sm:flex-row sm:space-x-4">

                        <!--required-->
                        <div class="flex flex-col w-full sm:w-1/2 p-2 pt-1 pb-4 border-2 rounded-md border-[#e0e0e0] shadow-none hover:shadow-lg flex-shrink pt-2">
                          <FormField v-slot="{ field }" name="requiredFeetCorner.value1">
                            <FormItem>
                              <FormLabel>Required</FormLabel>
                              <FormControl>
                                <Input v-model="formData.requiredFeetCornervalue1" v-bind="field" 
                                  class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                        focus:outline-none 
                                        hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300" 
                                  placeholder="Feet"/>
                              </FormControl>
                            </FormItem>
                        </FormField>
                        <Separator label="Or" class="mt-4 mb-2 bg-gray-400/50 font-medium " /> 
                        <FormField v-slot="{ field }" name="requiredFeetCorner.value2">
                          <FormItem>
                            <FormControl> 
                              <Input v-model="formData.requiredFeetCornervalue2" v-bind="field"  
                                class="mt-3 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                  focus:outline-none 
                                  hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300"
                                  placeholder="Type Here"/>
                            </FormControl>
                          </FormItem>
                        </FormField>
                        </div>


                        <!--existing -->
                        <div class="flex flex-col w-full sm:w-1/2 p-2 pt-1 pb-4 border-2 rounded-md border-[#e0e0e0] shadow-none hover:shadow-lg flex-shrink pt-2">
                          <FormField v-slot="{ field }" name="existingFeetCorner.value1">
                            <FormItem>
                              <FormLabel>Existing</FormLabel>
                              <FormControl>
                                <Input v-model="formData.existingFeetCornervalue1" v-bind="field" 
                                  class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                        focus:outline-none 
                                        hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300" 
                                  placeholder="Feet"/>
                              </FormControl>
                            </FormItem>
                        </FormField>
                        <Separator label="Or" class="mt-4 mb-2 bg-gray-400/50 font-medium " /> 
                        <FormField v-slot="{ field }" name="existingFeetCorner.value2">
                          <FormItem>
                            <FormControl> 
                              <Input v-model="formData.existingFeetCornervalue2" v-bind="field"  
                                class="mt-3 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                  focus:outline-none 
                                  hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300"
                                  placeholder="Type Here"/>
                            </FormControl>
                          </FormItem>
                        </FormField>
                      </div>
                      <!--end of existing-->
                      </div>
                      <!--end of card row component-->

                      <!--card row component-->
                      <h2 class="text-lg font-semibold text-gray-900 mb-2 mt-6">Minimum Interior Side</h2>
                      <hr class="w-full border-t border-gray-300 mb-4">
                      
                      <div class="flex flex-col sm:flex-row sm:space-x-4">

                        <!--required-->
                        <div class="flex flex-col w-full sm:w-1/2 p-2 pt-1 pb-4 border-2 rounded-md border-[#e0e0e0] shadow-none hover:shadow-lg flex-shrink pt-2">
                          <FormField v-slot="{ field }" name="requiredFeetInterior.value1">
                            <FormItem>
                              <FormLabel>Required</FormLabel>
                              <FormControl>
                                <Input v-model="formData.requiredFeetInteriorvalue1" v-bind="field" 
                                  class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                        focus:outline-none 
                                        hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300" 
                                  placeholder="Feet"/>
                              </FormControl>
                            </FormItem>
                        </FormField>
                        <Separator label="Or" class="mt-4 mb-2 bg-gray-400/50 font-medium " /> 
                        <FormField v-slot="{ field }" name="requiredFeetInterior.value2">
                          <FormItem>
                            <FormControl> 
                              <Input v-model="formData.requiredFeetInteriorvalue2" v-bind="field"  
                                class="mt-3 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                  focus:outline-none 
                                  hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300"
                                  placeholder="Type Here"/>
                            </FormControl>
                          </FormItem>
                        </FormField>
                        </div>


                        <!--existing -->
                        <div class="flex flex-col w-full sm:w-1/2 p-2 pt-1 pb-4 border-2 rounded-md border-[#e0e0e0] shadow-none hover:shadow-lg flex-shrink pt-2">
                          <FormField v-slot="{ field }" name="existingFeetInterior.value1">
                            <FormItem>
                              <FormLabel>Existing</FormLabel>
                              <FormControl>
                                <Input v-model="formData.existingFeetInteriorvalue1" v-bind="field" 
                                  class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                        focus:outline-none 
                                        hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300" 
                                  placeholder="Feet"/>
                              </FormControl>
                            </FormItem>
                        </FormField>
                        <Separator label="Or" class="mt-4 mb-2 bg-gray-400/50 font-medium " /> 
                        <FormField v-slot="{ field }" name="existingFeetInterior.value2">
                          <FormItem>
                            <FormControl> 
                              <Input v-model="formData.existingFeetInteriorvalue2" v-bind="field"  
                                class="mt-3 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                  focus:outline-none 
                                  hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300"
                                  placeholder="Type Here"/>
                            </FormControl>
                          </FormItem>
                        </FormField>
                      </div>
                      <!--end of existing-->
                      </div>
                      <!--end of card row component-->

                      <!--card row component-->
                      <h2 class="text-lg font-semibold text-gray-900 mb-2 mt-6">Minimum Rear</h2>
                      <hr class="w-full border-t border-gray-300 mb-4">
                      
                      <div class="flex flex-col sm:flex-row sm:space-x-4 mb-4">

                        <!--required-->
                        <div class="flex flex-col w-full sm:w-1/2 p-2 pt-1 pb-4 border-2 rounded-md border-[#e0e0e0] shadow-none hover:shadow-lg flex-shrink pt-2">
                          <FormField v-slot="{ field }" name="requiredFeetRear.value1">
                            <FormItem>
                              <FormLabel>Required</FormLabel>
                              <FormControl>
                                <Input v-model="formData.requiredFeetRearvalue1" v-bind="field" 
                                  class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                        focus:outline-none 
                                        hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300" 
                                  placeholder="Feet"/>
                              </FormControl>
                            </FormItem>
                        </FormField>
                        <Separator label="Or" class="mt-4 mb-2 bg-gray-400/50 font-medium " /> 
                        <FormField v-slot="{ field }" name="requiredFeetRear.value2">
                          <FormItem>
                            <FormControl> 
                              <Input v-model="formData.requiredFeetRearvalue2" v-bind="field"  
                                class="mt-3 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                  focus:outline-none 
                                  hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300"
                                  placeholder="Type Here"/>
                            </FormControl>
                          </FormItem>
                        </FormField>
                        </div>


                        <!--existing -->
                        <div class="flex flex-col w-full sm:w-1/2 p-2 pt-1 pb-4 border-2 rounded-md border-[#e0e0e0] shadow-none hover:shadow-lg flex-shrink pt-2">
                          <FormField v-slot="{ field }" name="existingFeetRear.value1">
                            <FormItem>
                              <FormLabel>Existing</FormLabel>
                              <FormControl>
                                <Input v-model="formData.existingFeetRearvalue1" v-bind="field" 
                                  class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                        focus:outline-none 
                                        hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300" 
                                  placeholder="Feet"/>
                              </FormControl>
                            </FormItem>
                        </FormField>
                        <Separator label="Or" class="mt-4 mb-2 bg-gray-400/50 font-medium " /> 
                        <FormField v-slot="{ field }" name="existingFeetRear.value2">
                          <FormItem>
                            <FormControl> 
                              <Input v-model="formData.existingFeetRearvalue2" v-bind="field"  
                                class="mt-3 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                  focus:outline-none 
                                  hover:border-gray-400 focus:border-blue-400/50 bg-white border-gray-300"
                                  placeholder="Type Here"/>
                            </FormControl>
                          </FormItem>
                        </FormField>
                      </div>
                      <!--end of existing-->
                      </div>
                      <!--end of card row component-->

                      <FormField v-slot="{ field }" name="step4UseConforming">
                        <FormItem>
                          <FormLabel class="text-md mb-2 mt-6">Does the Building Conform to Setback Requirements?</FormLabel>
                          <FormControl>
                            <ToggleGroup v-model="formData.step4UseConforming" type="single" v-bind="field" class="flex gap-4">
                              <ToggleGroupItem 
                                value="Yes" 
                                :class="{'selected': formData.step4UseConforming === 'Yes'}"
                                class="toggle-group-item mt-1 p-2 w-full border border-gray-300 rounded-md text-[16px] shadow-sm focus:outline hover:border-gray-400"
                              >
                                Yes
                              </ToggleGroupItem>
                              <ToggleGroupItem 
                                value="No" 
                                :class="{'selected': formData.step4UseConforming === 'No'}"
                                class="toggle-group-item mt-1 p-2 w-full border border-gray-300 rounded-md text-[16px] shadow-sm focus:outline hover:border-gray-400"
                              >
                                No
                              </ToggleGroupItem>
                            </ToggleGroup>
                          </FormControl>
                          <FormMessage />
                        </FormItem>
                      </FormField>

                      <FormField v-slot="{ field }" name="step4why">
                        <FormItem>
                          <FormLabel>Why</FormLabel>
                          <FormControl>
                            <Input v-model="formData.step4why" v-bind="field"
                              class="mt-1 p-2 pt-1 w-full border rounded-md text-[16px] shadow-sm 
                                     focus:outline-none focus:border-blue-400/50 
                                     hover:border-gray-400 bg-white border-gray-300" 
                              placeholder="Type Here"/>
                          </FormControl>
                          <FormMessage />
                        </FormItem>
                      </FormField>
                      
                      
                    </div>




                    <!-- End of Form -->
                  </div>
                </transition>
              </CardContent>
            </Card>

             <!-- Navigation Buttons moved here -->
          <div class="flex justify-end space-x-3 mt-4 mb-8">
            <Button 
              v-if="currentStep > 0" 
              @click="prevStep" 
              type="button"
              variant="outline"
              class="bg-gray-200 text-black-900 transition-colors duration-300 ease-in hover:bg-gray-100 text-[16px]"
            >
              Previous
            </Button>
            <Button 
              v-if="currentStep < steps.length - 1" 
              @click="nextStep" 
              type="button"
              class="bg-blue-600 text-white transition-colors duration-300 ease-in hover:bg-blue-800 text-[16px]"
              :disabled="!meta.valid"
            >
              Next
            </Button>
            <Button 
              v-if="currentStep === steps.length - 1" 
              type="submit"
              class="bg-green-600 text-white transition-colors duration-300 ease-in hover:bg-green-800 text-[16px]"
              :disabled="!meta.valid || isSubmitting"
            >
              {{ isSubmitting ? 'Submitting...' : 'Submit' }}
            </Button>
          </div>


          </div>
        </main>

        <!-- Footer with buttons -->

      </div>
    </Form>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue';
import { Form } from 'vee-validate';
import * as zod from 'zod';
import { toTypedSchema } from '@vee-validate/zod';
import html2pdf from 'html2pdf.js';
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import { FormField, FormItem, FormLabel, FormControl, FormMessage } from '@/components/ui/form';
import { ScrollArea } from '@/components/ui/scroll-area';
import { CheckIcon, CircleIcon, DotIcon } from '@radix-icons/vue';
import CustomProgressBar from './CustomProgressBar.vue';
import { ToggleGroup, ToggleGroupItem } from '@/components/ui/toggle-group';
import { Textarea } from '@/components/ui/textarea';
import { TextareaAutosize } from '@/components/ui/textarea-autosize';
import { Card, CardHeader, CardTitle, CardDescription, CardContent } from '@/components/ui/card';
import { Toggle } from '@/components/ui/toggle';
import { Separator } from '@/components/ui/separator';

import { collection, addDoc } from 'firebase/firestore';
import { db } from '@/firebase.config';

const steps = ['Subject Property', 'Zoning District', 'Adjacent Zoning', 'Building Setback Requirements'];
const currentStep = ref(0);

const formData = reactive({
  propertyAddress: '',
  municipality: '',
  county: '',
  state: '',
  assessorParcelNumber: '',
  yearBuilt: null as number | null,
  existingLandUse: '',
  zoningJurisdiction: '',
  zoningDistrict: '',
  overlayDistrict: '',
  overlayZone: '',
  adoptedDate: null as number | null,
  amendedDate: null as number | null,
  step2UsePermitted: '',
  step2why: '',
  step2UseConforming: '',
  zoningNorth: '',
  zoningDistrictNorth: '',
  zoningSouth: '',
  zoningDistrictSouth: '',
  zoningEast: '',
  zoningDistrictEast: '',
  zoningWest: '',
  zoningDistrictWest: '',
  parcelArea: '',
  parcelAreaUnit: '',
  step4Per: '',
  requiredFeetFrontvalue1: '',
  requiredFeetFrontvalue2: '',
  existingFeetFrontvalue1: '',
  existingFeetFrontvalue2: '',
  requiredFeetCornervalue1: '',
  requiredFeetCornervalue2: '',
  existingFeetCornervalue1: '',
  existingFeetCornervalue2: '',
  requiredFeetInteriorvalue1: '',
  requiredFeetInteriorvalue2: '',
  existingFeetInteriorvalue1: '',
  existingFeetInteriorvalue2: '',
  requiredFeetRearvalue1: '',
  requiredFeetRearvalue2: '',
  existingFeetRearvalue1: '',
  existingFeetRearvalue2: '',
  step4UseConforming: '',
  step4why: '',
});

const formSchema = [
  zod.object({
    propertyAddress: zod.string().min(1, 'Property address is required'),
    municipality: zod.string().min(1, 'Municipality is required'),
    county: zod.string().min(1, 'County is required'),
    state: zod.string().min(1, 'State is required'),
    assessorParcelNumber: zod.string().min(1, 'Assessor Parcel Number is required'),
    yearBuilt:zod
      .number({ invalid_type_error: 'Year Built must be a number' })
      .min(1900, { message: 'Year Built must be at least 1900' })
      .max(new Date().getFullYear(), { message: 'Year Built cannot be in the future' }),
    existingLandUse: zod.string().min(1, 'Existing Land Use is required'),
  }),
  zod.object({
    zoningJurisdiction: zod.string().min(1, 'Zoning Jurisdiction is required'),
    zoningDistrict: zod.string().min(1, 'Zoning District is required'),
    overlayDistrict: zod.string().optional(),
    overlayZone: zod.string().optional(),
    adoptedDate: zod
      .number({ invalid_type_error: 'Year Built must be a number' })
      .min(1900, { message: 'Year Built must be at least 1900' })
      .max(new Date().getFullYear(), { message: 'Year Built cannot be in the future' }),
      amendedDate: zod
      .number({ invalid_type_error: 'Amended Date must be a number' })
      .min(1900, { message: 'Amended Date must be at least 1900' })
      .max(new Date().getFullYear(), { message: 'Amended Date cannot be in the future' })
      .optional()
      .nullable(),
    step2UsePermitted: zod.enum(['Yes', 'No'], { required_error: 'Please select if the current use is permitted' }),
    step2why: zod.string().min(1, 'Please explain why'),
    step2UseConforming: zod.enum(['Yes', 'No'], { required_error: 'Please select if the current use is conforming' }),

  }),
  zod.object({
    zoningNorth: zod.string().min(1, 'North Zoning is required'),
    zoningDistrictNorth: zod.string().min(1, 'North Zoning District is required'),
    zoningSouth: zod.string().min(1, 'South Zoning is required'),
    zoningDistrictSouth: zod.string().min(1, 'South Zoning District is required'),
    zoningEast: zod.string().min(1, 'East Zoning is required'),
    zoningDistrictEast: zod.string().min(1, 'East Zoning District is required'),
    zoningWest: zod.string().min(1, 'West Zoning is required'),
    zoningDistrictWest: zod.string().min(1, 'West Zoning District is required'),
    parcelArea: zod.string().min(1, 'Parcel Area is required'),
    parcelAreaUnit: zod.string().min(1, 'Parcel Area Unit is required'),
  }),
  zod.object({
    step4Per: zod.string().optional(),
    requiredFeetFrontvalue1: zod.string().optional(),
    requiredFeetFrontvalue2: zod.string().optional(),
    existingFeetFrontvalue1: zod.string().optional(),
    existingFeetFrontvalue2: zod.string().optional(),
    requiredFeetCornervalue1: zod.string().optional(),
    requiredFeetCornervalue2: zod.string().optional(),
    existingFeetCornervalue1: zod.string().optional(),
    existingFeetCornervalue2: zod.string().optional(),
    requiredFeetInteriorvalue1: zod.string().optional(),
    requiredFeetInteriorvalue2: zod.string().optional(),
    existingFeetInteriorvalue1: zod.string().optional(),
    existingFeetInteriorvalue2: zod.string().optional(),
    requiredFeetRearvalue1: zod.string().optional(),
    requiredFeetRearvalue2: zod.string().optional(),
    existingFeetRearvalue1: zod.string().optional(),
    existingFeetRearvalue2: zod.string().optional(),
    step4UseConforming: zod.enum(['Yes', 'No'], { required_error: 'Please select if the building conforms to setback requirements' }),
    step4why: zod.string().optional(),
  }),
];

const nextStep = () => {
  if (currentStep.value < steps.length - 1) {
    currentStep.value++;
  }
};

const prevStep = () => {
  if (currentStep.value > 0) {
    currentStep.value--;
  }
};

const isSubmitting = ref(false);

const submitForm = async () => {
  isSubmitting.value = true;
  try {
    console.log('Form values:', formData);

    // Save to Firebase
    const docRef = await addDoc(collection(db, "zoningReports"), {
      ...formData,
      createdAt: new Date()
    });
    console.log("Document written with ID: ", docRef.id);

    // Generate PDF
    const element = document.createElement('div');
    element.innerHTML = generateReportHTML(formData);

    const opt = {
      margin: 20,
      filename: 'zoning_report.pdf',
      image: { type: 'jpeg', quality: 0.98 },
      html2canvas: { scale: 2 },
      jsPDF: { unit: 'mm', format: 'a4', orientation: 'portrait' }
    };

    await html2pdf().from(element).set(opt).save();

    console.log('PDF generated');
    console.log('Form submitted successfully and saved to Firebase');
  } catch (error) {
    console.error('Error during form submission:', error);
  } finally {
    isSubmitting.value = false;
  }
};

function generateReportHTML(formData: typeof formData) {
  return `
    <h1>Zoning Report</h1>
    <h2>Subject Property</h2>
    <p><strong>Property Address:</strong> ${formData.propertyAddress}</p>
    <p><strong>Municipality:</strong> ${formData.municipality}</p>
    <p><strong>County:</strong> ${formData.county}</p>
    <p><strong>State:</strong> ${formData.state}</p>
    <p><strong>Assessor Parcel Number:</strong> ${formData.assessorParcelNumber}</p>
    <p><strong>Year Built:</strong> ${formData.yearBuilt}</p>
    <p><strong>Existing Land Use:</strong> ${formData.existingLandUse}</p>

    <h2>Zoning District</h2>
    <p><strong>Zoning Jurisdiction:</strong> ${formData.zoningJurisdiction}</p>
    <p><strong>Zoning District:</strong> ${formData.zoningDistrict}</p>
    ${formData.overlayDistrict ? `<p><strong>Overlay District:</strong> ${formData.overlayDistrict}</p>` : ''}
    ${formData.overlayZone ? `<p><strong>Overlay Zone:</strong> ${formData.overlayZone}</p>` : ''}
    <p><strong>Adopted Date:</strong> ${formData.adoptedDate}</p>
    ${formData.amendedDate ? `<p><strong>Amended Date:</strong> ${formData.amendedDate}</p>` : ''}
    <p><strong>Is Current Use Permitted:</strong> ${formData.step2UsePermitted}</p>
    <p><strong>Why:</strong> ${formData.step2why}</p>
    <p><strong>Is Current Use Conforming:</strong> ${formData.step2UseConforming}</p>


    <h2>Adjacent Zoning</h2>
    ${formData.zoningNorth ? `<p><strong>North Zoning:</strong> ${formData.zoningNorth}</p>` : ''}
    ${formData.zoningDistrictNorth ? `<p><strong>North Zoning District:</strong> ${formData.zoningDistrictNorth}</p>` : ''}
    ${formData.zoningSouth ? `<p><strong>South Zoning:</strong> ${formData.zoningSouth}</p>` : ''}
    ${formData.zoningDistrictSouth ? `<p><strong>South Zoning District:</strong> ${formData.zoningDistrictSouth}</p>` : ''}
    ${formData.zoningEast ? `<p><strong>East Zoning:</strong> ${formData.zoningEast}</p>` : ''}
    ${formData.zoningDistrictEast ? `<p><strong>East Zoning District:</strong> ${formData.zoningDistrictEast}</p>` : ''}
    ${formData.zoningWest ? `<p><strong>West Zoning:</strong> ${formData.zoningWest}</p>` : ''}
    ${formData.zoningDistrictWest ? `<p><strong>West Zoning District:</strong> ${formData.zoningDistrictWest}</p>` : ''}

    <h2>Parcel Area</h2>
    <p><strong>Parcel Area:</strong> ${formData.parcelArea} ${formData.parcelAreaUnit}</p>

    <h2>Building Setback Requirements</h2>
    <p><strong>Per:</strong> ${formData.step4Per}</p>

   <h3>Minimum Front from Street</h3>
    <p><strong>Required:</strong></p>
    ${formData.requiredFeetFrontvalue1 ? `<p>${formData.requiredFeetFrontvalue1} feet</p>` : ''}
    ${!formData.requiredFeetFrontvalue1 && formData.requiredFeetFrontvalue2 ? `<p>${formData.requiredFeetFrontvalue2}</p>` : ''}
    <p><strong>Existing:</strong></p>
    ${formData.existingFeetFrontvalue1 ? `<p>${formData.existingFeetFrontvalue1} feet</p>` : ''}
    ${!formData.existingFeetFrontvalue1 && formData.existingFeetFrontvalue2 ? `<p>${formData.existingFeetFrontvalue2} feet</p>` : ''}

    <h3>Minimum Corner Side</h3>
    <p><strong>Required:</strong></p>
    ${formData.requiredFeetCornervalue1 ? `<p>${formData.requiredFeetCornervalue1} feet</p>` : ''}
    ${!formData.requiredFeetCornervalue1 && formData.requiredFeetCornervalue2 ? `<p>${formData.requiredFeetCornervalue2}</p>` : ''}
    <p><strong>Existing:</strong></p>
    ${formData.existingFeetCornervalue1 ? `<p>${formData.existingFeetCornervalue1} feet</p>` : ''}
    ${!formData.existingFeetCornervalue1 && formData.existingFeetCornervalue2 ? `<p>${formData.existingFeetCornervalue2} feet</p>` : ''}

    <h3>Minimum Interior Side</h3>
    <p><strong>Required:</strong></p>
    ${formData.requiredFeetInteriorvalue1 ? `<p>${formData.requiredFeetInteriorvalue1} feet</p>` : ''}
    ${!formData.requiredFeetInteriorvalue1 && formData.requiredFeetInteriorvalue2 ? `<p>${formData.requiredFeetInteriorvalue2}</p>` : ''}
    <p><strong>Existing:</strong></p>
    ${formData.existingFeetInteriorvalue1 ? `<p>${formData.existingFeetInteriorvalue1} feet</p>` : ''}
    ${!formData.existingFeetInteriorvalue1 && formData.existingFeetInteriorvalue2 ? `<p>${formData.existingFeetInteriorvalue2} feet</p>` : ''}

    <h3>Minimum Rear</h3>
    <p><strong>Required:</strong></p>
    ${formData.requiredFeetRearvalue1 ? `<p>${formData.requiredFeetRearvalue1} feet</p>` : ''}
    ${!formData.requiredFeetRearvalue1 && formData.requiredFeetRearvalue2 ? `<p>${formData.requiredFeetRearvalue2}</p>` : ''}
    <p><strong>Existing:</strong></p>
    ${formData.existingFeetRearvalue1 ? `<p>${formData.existingFeetRearvalue1} feet</p>` : ''}
    ${!formData.existingFeetRearvalue1 && formData.existingFeetRearvalue2 ? `<p>${formData.existingFeetRearvalue2} feet</p>` : ''}


    <p><strong>Does the Building Conform to Setback Requirements?</strong> ${formData.step4UseConforming}</p>
    <p><strong>Why:</strong> ${formData.step4why}</p>
    
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
  `;
}
</script>

<style scoped>
.slide-enter-active,
.slide-leave-active {
  transition: all 0.3s ease;
}

.slide-enter-from {
  opacity: 0;
  transform: translateX(30px);
}

.slide-leave-to {
  opacity: 0;
  transform: translateX(-30px);
}

.hover\:shadow-md:hover {
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06) !important;
}

.transition-shadow {
  transition-property: box-shadow !important;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1) !important;
  transition-duration: 300ms !important;
}

.toggle-group-item {
  transition: background-color 0.3s ease, color 0.3s ease;
}

.toggle-group-item.selected {
  background-color: #007bff; /* Your selected background color */
  color: white; /* Your selected text color */
}

.toggle-group-item:not(.selected) {
  background-color: white;
  color: black;
}

.toggle-group-item:hover {
  border-color: #007bff; /* Your hover border color */
}
</style>
