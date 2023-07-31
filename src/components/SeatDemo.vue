
<template>
    <div class="stepsdemo-content">
        <Card>
            <template v-slot:title>
                Serviços de Calibração
            </template>
            <template v-slot:subtitle>
                Escolha os serviços
            </template>
            <template v-slot:content>
                <div class="p-fluid formgrid grid">
                    <div class="field col">
                        <Tree v-model:selectionKeys="servicosSelecionados" :value="dados" selectionMode="checkbox" class="w-full"></Tree>                        
                    </div>
                </div>
            </template>
            <template v-slot:footer>
                <div class="grid grid-nogutter justify-content-between">
                    <Button label="Voltar" @click="prevPage()" icon="pi pi-angle-left" />
                    <Button label="Próximo" @click="nextPage()" icon="pi pi-angle-right" iconPos="right" />
                </div>
            </template>
        </Card>
    </div>
</template>

<script>
export default {
    data () {
        return {
            selectedClass: '',
            classes: [
                {name: 'First Class', code: 'A', factor: 1},
                {name: 'Second Class', code: 'B', factor: 2},
                {name: 'Third Class', code: 'C', factor: 3}
            ],
            vagons: [],
            selectedVagon: '',
            seats: [],
            selectedSeat: '',
            servicosSelecionados: null,
            dados: [
                {
                    key: '0',
                    label: '0001 - Paquimetro - Paquimetro XPTO',
                    data: '0001',
                    icon: 'pi pi-fw pi-inbox',
                    children: [
                        {
                            key: '0-0',
                            label: 'Serviço 001',
                            data: 'Serv001',
                            icon: 'pi pi-fw pi-cog',
                        },
                        {
                            key: '0-1',
                            label: 'Serviço 002',
                            data: 'Serv002',
                            icon: 'pi pi-fw pi-cog',
                        }
                    ]
                },
                {
                    key: '1',
                    label: '0002 - Calibrador de Boca - Calibrador de Boca XPTO',
                    data: '0002',
                    icon: 'pi pi-fw pi-inbox',
                    children: [
                        {
                            key: '1-0',
                            label: 'Serviço 003',
                            data: 'Serv003',
                            icon: 'pi pi-fw pi-cog',
                        },
                        {
                            key: '1-1',
                            label: 'Serviço 004',
                            data: 'Serv004',
                            icon: 'pi pi-fw pi-cog',
                        }
                    ]
                },
                {
                    key: '2',
                    label: '0003 - Relógio Comparador - Relógio Comparador XPTO',
                    data: '0003',
                    icon: 'pi pi-fw pi-inbox',
                    children: [
                        {
                            key: '2-0',
                            label: 'Serviço 005',
                            data: 'Serv005',
                            icon: 'pi pi-fw pi-cog',
                        },
                        {
                            key: '2-1',
                            label: 'Serviço 006',
                            data: 'Serv006',
                            icon: 'pi pi-fw pi-cog',
                        }
                    ]
                }                                
            ]
        }
    },
    methods: {
        nextPage() {
            this.$emit('next-page', {pageIndex: 1});
        },
        prevPage() {
            this.$emit('prev-page', {pageIndex: 1});
        }
    }
}
</script>
